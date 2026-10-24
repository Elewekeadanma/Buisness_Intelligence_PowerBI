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
Data Source 
: A folder of raw CSV files, which contain information about transaction
and return records, products, customers, and sales territories.

Data Model Overview
The Power BI data model was built using  Snowflake Schema principles for performance and scalability:
A star schema was created first by creating relationships between the Sales, Calendar, customer, Product and Territories tables as shown below. 

__<img width="975" height="458" alt="image" src="https://github.com/user-attachments/assets/3574de97-8d40-4df0-8a50-830e5751818b" />
_______________________________________________________________________________________________________________________________________________________________________________________
And then all three product tables were connected in a snowflake schema as highlighted below
<img width="975" height="546" alt="image" src="https://github.com/user-attachments/assets/07896820-8a76-4720-ba84-baebe137f3a1" />

•	Fact Tables: Sales Data, Returns Data
•
Dimension Tables: Territory Lookup, Customer Lookup, Calendar Lookup, Product Lookup,  Product Categories Lookup, Product Subcategories Lookup,
As shown below, the product lookup table also contains a foreign key of its own called product subcategory key and the product subcategory table also has a foreign key called product category key. This chain of relationships where we connect dimension tables to sub dimension tables gives us our Snowflake schema.

_________________________________________________________________________________________________________________________________________________________________________________________
A **MATRIX** visual in Power BI is designed to display data in a structured, pivot‑table‑style layout, making it ideal for exploring data across multiple dimensions.
 
<img width="975" height="516" alt="image" src="https://github.com/user-attachments/assets/5d2febd8-7951-45f3-be91-357b15dfaddf" />

Looking at the highlighted Matrix, the formatting in the Orders bars shows the relative differences in the number of orders for each product and thus we can decide which product we should make sure is always available. For the Return rate bar, the highest values had a very red color to highlight the bad ones.
Also, using the Top N filter, the matrix showed only the Top 10 highest orders sold, with Water Bottles at the top.

________________________________________________________________________________________________________________________________________________________________________________________
A **DONUT** visual in Power BI is designed to show how a whole is divided into parts, while keeping the focus on the proportions of each category.
<img width="1920" height="1128" alt="image" src="https://github.com/user-attachments/assets/8667b135-dd5d-42ad-982e-e93c536dd10d" />

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



