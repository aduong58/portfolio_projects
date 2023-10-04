Hello! Currently a work in progress, transferring information over from BigQuery and Tableau Desktop.

This is a complementary portion to the [Nexus Sales Analysis](https://github.com/aduong58/portfolio_projects/tree/main/Nexus-Sales-Analysis) project. This subsegment of the main project will contain:
1. SQL queries that were used for ad-hoc analysis before and during the Excel analysis.
2. Tableau dashboard created towards the end of the project for more visual analysis of the data.


## Ad-hoc Analysis using SQL
<details>
<summary>What are the monthly and quarterly sales trends for Macbooks sold in North America across all years </summary> <br>
  Insert notes for this questions here.
  
  ````sql
with quarterly_data as (
  SELECT date_trunc(orders.purchase_ts, quarter) as purchase_quarter,
    geo_lookup.region,
    round(sum(orders.usd_price)) as quarterly_sales,
    count(orders.usd_price) as order_count,
    round(avg(orders.usd_price)) as aov
  from elist.orders
  inner join elist.customers
    on customers.id = orders.customer_id
  left join elist.geo_lookup
    on customers.country_code = geo_lookup.country
  where lower(orders.product_name) like "%macbook%"
    and lower(geo_lookup.region) like "%na%"
  group by purchase_quarter, geo_lookup.region
  order by purchase_quarter desc
)

SELECT round(avg(quarterly_sales)) as average_quarterly_sales,
  avg(order_count) as avg_order_count,
  avg(aov) as avg_aov
from quarterly_data
  ```` 
</details>

<details>
<summary>What was the monthly refund rate for purchases made in 2020? How many refunds did we have each month in 2021 for Apple products?</summary> <br>
  Insert notes for this questions here.
  
  ````sql
  Insert SQL query here 
  ````
</details>

<details>
<summary>Are there certain products that are getting refunded more frequently than others? What are the top 3 most frequently refunded products across all years? What are the top 3 products that have the highest count of refunds?</summary> <br>
  Insert notes for this questions here.
  
  ````sql
  Insert SQL query here 
  ````
</details>

<details>
<summary>What’s the average order value across different account creation methods in the first two months of 2022? Which method had the most new customers in this time?</summary> <br>
  Insert notes for this questions here.
  
  ````sql
  Insert SQL query here 
  ````
</details>

<details>
<summary>What’s the average time between customer registration and placing an order?</summary> <br>
  Insert notes for this questions here.
  
  ````sql
  Insert SQL query here 
  ````
</details>

<details>
<summary>Which marketing channels perform the best in each region? Does the top channel differ across regions?</summary> <br>
  Insert notes for this questions here.
  
  ````sql
  Insert SQL query here 
  ````
</details>

<details>
<summary>For customers who purchased more than 4 orders across all years, what was the order ID, product, and purchase date of their most recent order?</summary> <br>
  Insert notes for this questions here.
  
  ````sql
  Insert SQL query here 
  ````
</details>

<details>
<summary>For each brand, which month in 2020 had the highest number of refunds, and how many refunds did that month have?</summary> <br>
  Insert notes for this questions here.
  ````sql
  Insert SQL query here 
  ````
</details>

