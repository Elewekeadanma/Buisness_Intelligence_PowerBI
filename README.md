This project shows a comprehensive Power BI dashboard developed for a fictional global manufacturing company that produces cycling equipment and accessories.  
## Objective
The project aims to monitor key performance indicators, to help the management team track their KPIs, things like sales, revenue, profit and returns, compare performance across regions, analyze product-level trends, and identify high-value customers. This means that the dashboard is going to be exploratory as well as explanatory.

## Goals
- Track KPIs
- Compare regional performance
- Analyze product level trends 
- Identify high-value customers

### Tools & Technologies
![Power BI](https://img.shields.io/badge/PowerBI-F2C811?logo=powerbi&logoColor=black)

| Tool | Use |
|--------|------:|
| Power BI Desktop | Data modeling, dashboard creation |
| Power Query | Data transformation and cleaning |
| DAX | Business logic and KPIs |
| Power BI Service | For live publishing, sharing, and cloud-based report consumption |

________________________________________________________________________________________________________________________________________________________________________________________
### Data Source 
A folder of raw CSV files, which contain information about transaction and return records, products, customers, and sales territories.

### Data Model Overview
The Power BI data model was built using  Snowflake Schema principles for performance and scalability:
A **Star** schema was created first by creating relationships between the Sales, Calendar, customer, Product and Territories tables as shown below. 

<img width="975" height="458" alt="image" src="https://github.com/user-attachments/assets/3574de97-8d40-4df0-8a50-830e5751818b" />
_______________________________________________________________________________________________________________________________________________________

Then all three product tables were connected in a **Snowflake** schema as highlighted below
<img width="975" height="546" alt="image" src="https://github.com/user-attachments/assets/07896820-8a76-4720-ba84-baebe137f3a1" />

**Fact Tables**: Sales Data, Returns Data

**Dimension Tables**: Territory Lookup, Customer Lookup, Calendar Lookup, Product Lookup,  Product Categories Lookup, Product Subcategories Lookup,

As shown below, the product lookup table also contains a foreign key of its own called product subcategory key and the product subcategory table also has a foreign key called product category key. This chain of relationships where we connect dimension tables to sub dimension tables gives us our Snowflake schema.

_________________________________________________________________________________________________________________________________________________________________________________________
Key Columns Include:

* SalesTerritoryKey
* CustomerKey
* ProductKey
* ProductCategoriesKey
* Product SubcategoriesKey

  
**Hidden keys**

Also note that some fields containing  were hidden from report view so that I don’t make a mistake of filtering on a foreign key from a data table instead of a primary key from a lookup table.
* From the Sales data table, I removed the customer key, order date, product key, stock date, and territory key.
* From the returns table, I removed the product key, return date and territory key.
* From the product table, I removed the subcategory key.
* From the product subcategories table, I removed the Product category key.


________________________________________________________________________________________________________________________________________________________________________________________
### Data Cleaning and Transformation 
- Column headers were promoted.
- Product Key and ProductSubcategorykey were changed from number to text fields.
- ProductCost and ProductPrice columns were changed from decimal to currencies.
- A redundant column ProductSize was also removed.
- A new column SKU Type was added by extracting all characters before the dash in the Product SKU column, then the SKU Type was calculated to return all characters before the second dash, instead of the first.
- The zeros (0) in the Product Style column was replaced with “NA”.
- The Domain Name column was added by duplicating the email address column, remove all text/characters except the domain name and capitalizing.
- The following columns were added to the calendar table
Month Name (e.g March), Month Number (e.g “1”)
Start of Year (e.g. “1/1/2020”), Year (e.g “2020”)
- A conditional column “Quantity Type” was added in the Sales table with 2 options Single Item , Multiple Items
- A date hierarchy column was created with the hierarchy in the following order:  
•	Start of year  
•	start of month  
•	start of week  
•	date

- A column, "Education Category" was created using the Switch function.
- A column "SKU Category" was created by returning any number of characters before the first hyphen in the Product SKU column.
- A column "Birth Year" was created in the Customer Lookup to extract only the year from the Birthdate column.


## ANALYTICAL APPROACH 
The dashboard is designed into 4 tabs.

## Executive Dashboard  
This dashboard page gives an executive overview of Adventure Works sales performance, combining revenue, profitability, order volume, returns, trends, product performance, and category performance.

<img width="1617" height="1007" alt="image" src="https://github.com/user-attachments/assets/c223dfdc-2878-4153-8ac3-3257707ffa67" />

* Revenue: $24.9M
* Total Profit: $10.5M, indicating strong profitability relative to revenue.
* Orders: 25.2K
* Return Rate: 2.2%

Key insights
Revenue is trending upward.

The revenue trend shows overall growth from 2020 through 2022. After fluctuations during 2020 and early 2021, revenue accelerates significantly from mid-2021, reaching approximately $1.8M per month toward the end of the period.

**Accessories** generate the most orders.
Order volume by category is:
1.	Accessories: 17K
2.	Bikes: 14K
3.	Clothing: 7K
Accessories therefore lead order volume by a noticeable margin.



**Latest monthly performance**
The bottom KPIs indicate:
This section provides a month-over-month performance snapshot across revenue, orders, and returns:
•	Monthly Revenue: Revenue reached $1.83M, up from $1.77M in the previous month, representing 3.31% growth.
•	Monthly Orders: Orders declined slightly to 2,146, compared with 2,165 in the previous month, a 0.88% decrease.
•	Monthly Returns: Returns decreased from 169 to 166, meaning 3 fewer returns than the previous month.

Key takeaway
Overall, the month shows positive revenue growth despite slightly fewer orders. Revenue increased by 3.31% while order volume fell by less than 1%. Returns also declined slightly, which is favorable.
Note: The Monthly Returns card displays “+1.78%”, but because returns decreased from 169 to 166, the direction appears inconsistent. If the measure is intended to show month-over-month change in the number of returns, it would be approximately -1.78%.

Product highlights
•	Most Ordered Product Type: Tires and Tubes
•	Most Returned Product Type: Bib-Shorts
Overall takeaway
Business performance is positive, with $24.9M in revenue, $10.5M in profit, and revenue continuing to grow. Despite a slight decline in monthly order volume, monthly revenue increased 3.31%, which could indicate higher revenue per order. Returns remain relatively low overall at 2.2%, although several helmet products have return rates above 3% and could be investigated further. Accessories are the strongest category by order volume.

## Map Dashboard
This **Map dashboard** provides a geographic view of total orders, showing how order volume is distributed across the main sales regions and countries.
<img width="975" height="609" alt="image" src="https://github.com/user-attachments/assets/34cef23c-271b-4586-a522-d8da68719d62" />

**Dashboard summary**
* The map displays Total Orders by Country, with larger blue bubbles representing higher order volumes.
* Orders are shown across North America, Europe, and the Pacific region.
* The United States has the largest bubble, indicating the highest order volume among the countries displayed.
* Australia also shows a relatively high concentration of orders.
* Canada has a smaller order volume than the United States.
* In Europe, orders are distributed across the United Kingdom, France, and Germany, with relatively similar-sized bubbles.
* The region selector at the top allows the dashboard to be filtered by Europe, North America, or Pacific, or viewed collectively using Select all.

#### Key takeaway
Order activity is geographically diversified, but the United States appears to be the strongest market by order volume. Australia is another significant market, while European orders are spread across the United Kingdom, France, and Germany.

#### Recommendations

The geographical analysis shows that order activity is concentrated primarily in the United States, with Australia also representing a significant market. The business should protect performance in these strong markets while investigating growth opportunities across the United Kingdom, France, and Germany. Further analysis of revenue, profitability, average order value, and returns by country is recommended before making regional investment decisions. 


## Product Detail Dashboard
This page is a Product Detail page, set the page type to Drill through and configured  drill through from Product Name. What this means is that users can right-click any instance of product name and use the Drill through option to navigate straight to the Product Detail report filtered on the product (in this case “Sport-100 Helmet, Black”)

<img width="804" height="509" alt="image" src="https://github.com/user-attachments/assets/8a0e8039-46ec-4012-9e88-44636778e021" />


### Key performance summary

<img width="579" height="179" alt="image" src="https://github.com/user-attachments/assets/682960d4-a5ee-4bf5-afc9-7e4e241ebc6b" />


<img width="580" height="172" alt="image" src="https://github.com/user-attachments/assets/22ba4975-46ff-424d-a193-813bc14e76b2" />

### Key business insights

**Orders are close to target, but there is still a gap.**

So the product needs approximately 8.4% more orders relative to the current 404 orders to reach the displayed target. This is not a severe underperformance, but there is room for improvement.

**Revenue is even closer to target**
Monthly Revenue is $4,067 against approximately $4,290.

That means revenue attainment is about:

$4,067 ÷ $4,290 = 94.8%

Only approximately:

$4,290 - $4,067 = $223

of additional monthly revenue is required to reach the target.

This is a positive sign because revenue is proportionally closer to target than order volume.

**Profit has generally improved during the period**
The Profit Trending chart shows profit rising approximately from:

January: $2.17K
February: $2.24K
March: $2.39K
April: $2.47K
May: $2.44K
June: $2.55K

The general direction is upward.

There is a small decline from April to May, followed by the strongest displayed value in June.

From January to June, the increase is roughly:

($2,550 - $2,170) ÷ $2,170 ≈ 17.5%

So profitability appears to have improved materially during the six-month period.

**Order volume is also trending upward**
The lower orders chart shows approximately:

344 → 352 → 359 → 391 → 391 → 393/394

The strongest improvement occurs between February and March.

This suggests that the improving profit trend is accompanied by increasing order volume rather than coming solely from price or margin changes.

However, the latest monthly orders shown on the gauge are 404, while the trend chart appears to end around the low 390s. I would verify whether the visuals are operating under the same date/filter context.

Insights
. Investigate the order shortfall
Investigate the May profit decline
Monitor returns alongside growth


## Customer Detail Dashboard
The dashboard provides a detailed view of the customer base by combining customer counts, revenue, purchasing behavior, demographics, and individual customer performance. It can be used to identify high-value customer segments and top customers, understand which groups generate the most orders, and support more targeted sales and customer-retention strategies.

<img width="1920" height="1128" alt="image" src="https://github.com/user-attachments/assets/8667b135-dd5d-42ad-982e-e93c536dd10d" />

**What the dashboard does**
*	Tracks overall customer performance: It shows 17.2K unique customers and approximately $1.1K revenue per customer, providing a quick view of the size and value of the customer base.
*	Analyzes customer trends over time: The line chart can switch between Total Customers and Revenue per Customer, allowing users to see how customer activity or value changes over the selected period.
*	Segments customers by income: The Orders by Income Level chart compares purchasing activity across Low, Average, and High income groups. The Average-income segment has the largest order volume shown at approximately 10.5K orders.
*	Analyzes orders by occupation: The dashboard compares orders across occupation groups. Professional customers represent the largest visible segment with approximately 7.1K orders, followed by Skilled Manual at 5.3K and Management at 3.9K.
*	Identifies high-value customers: The Top 100 Customers table ranks individual customers using orders and revenue, making it possible to identify customers who contribute the most to sales.
*	Highlights the top customer: A dedicated section identifies the top customer by revenue and displays the customer's corresponding order count and revenue, which are 6 orders and approximately $12.4K in the current view.
*	Supports time-based analysis: The Year control allows customer results to be filtered between 2021 and 2022.

