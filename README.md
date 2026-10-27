This is a global manufacturing company that produces cycling equipment and accessories.  
## Objective
The project aims to monitor key performance indicators—such as sales, revenue, profit, and returns—evaluate how different regions are performing, uncover trends at the product level, and pinpoint high‑value customers by leveraging data on transactions, returns, products, customers, and sales territories.

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


## Analytical Approach  
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

<img width="1920" height="1128" alt="image" src="https://github.com/user-attachments/assets/8667b135-dd5d-42ad-982e-e93c536dd10d" />

Latest monthly performance
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

## The Map dashboard







Using the donut visuals, we were able to show the composition of customers by Income level and Occupation.
The analysis tells us the customer with the highest revenue, in our case it was Mr Maurice Shan as shown in the textbox and table.

________________________________________________________________________________________________________________________________________________________________________________________
A **MAP** visual in Power BI is designed to show data in a geographic context, making it easy to understand how metrics vary across locations. The map visual, in this case was used to visualize data by continent and country and to compare performance across regions.


This image shows all the geographical locations, bubble size indicating the number of orders for each region.
<img width="975" height="609" alt="image" src="https://github.com/user-attachments/assets/34cef23c-271b-4586-a522-d8da68719d62" />

The second map visual shows Europe and countries in Europe with their corresponding total number of orders, United Kingdom having a total of 2771 orders.

<img width="975" height="609" alt="image" src="https://github.com/user-attachments/assets/efc472fc-96ad-4205-bba7-c6441d9c3a4b" />

_______________________________________________________________________________________________________________________________________________________________________________________
Another visualization in Power Bi is a **GUAGE** chart. A gauge visual in Power BI is designed to show progress toward a target in a simple, intuitive way. It’s one of the clearest visuals for communicating performance status at a glance and it is used for displaying a single KPI (e.g., sales, revenue, profit, utilization), showing how close the current value is to a goal, highlighting whether performance is low, on track, or exceeding expectations and providing a quick, dashboard‑friendly indicator of status

<img width="1920" height="1128" alt="image" src="https://github.com/user-attachments/assets/3272da38-fc0f-4b33-94c4-d8fd628fe6f6" />
The chart tells us that we are yet to hit our Monthly targets and Monthly Revenue for Bike Wash - Dissolver even though the Monthly Profit has been met. Using the slicer beside the guage chart, we can find out which products are hitting their targets or not. The unmet targets are shown in red while the met target is shown in black.



