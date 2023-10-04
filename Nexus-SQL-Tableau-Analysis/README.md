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
  with refund_rates_2020 as (
  select date_trunc(orders.purchase_ts, month) as sales_month, 
    round(count(order_status.refund_ts) / count(*), 4) as refund_rate
  from elist.orders
  left join elist.order_status
    on orders.id = order_status.id
  where extract(year from orders.purchase_ts) = 2020
  group by sales_month
  order by sales_month
),

apple_refunds_2021 as (
  select date_trunc(orders.purchase_ts, month) as sales_month,
    count(order_status.refund_ts) as refunds_count
  from elist.orders
  left join elist.order_status
    on orders.id = order_status.id
  where extract(YEAR from orders.purchase_ts) = 2021
    and (lower(orders.product_name) like "%apple%" 
    or lower(orders.product_name) like "%macbook%")
  group by sales_month
  order by sales_month
)

select * from apple_refunds_2021
  ````
</details>

<details>
<summary>Are there certain products that are getting refunded more frequently than others? What are the top 3 most frequently refunded products across all years? What are the top 3 products that have the highest count of refunds?</summary> <br>
  Insert notes for this questions here.
  
  ````sql
  select 
    CASE WHEN orders.product_name like "%\"\"%" THEN "27in 4K gaming monitor"
      ELSE orders.product_name
      END AS product_name_clean,
    count(order_status.refund_ts) as refund_count,
    round(count(order_status.refund_ts) / count(*), 4) as refund_rate
  from elist.orders
  left join elist.order_status
    on orders.id = order_status.id
  group by product_name_clean
  order by refund_rate desc
  -- order by refund_count desc
  ````
</details>

<details>
<summary>What’s the average order value across different account creation methods in the first two months of 2022? Which method had the most new customers in this time?</summary> <br>
  Insert notes for this questions here.
  
  ````sql
  with creation_method_count as (
  select 
    case when customers.account_creation_method is null then "unknown"
      else customers.account_creation_method
      end as account_creation_method_clean,
    round(avg(orders.usd_price), 2) as aov,
    count(*) as new_customer_count
  from elist.orders
  left join elist.customers
    on orders.customer_id = customers.id
  where customers.created_on between '2022-01-01' and '2022-02-28'
  group by account_creation_method_clean
  order by aov desc
)

select * from creation_method_count
  ````
</details>

<details>
<summary>What’s the average time between customer registration and placing an order?</summary> <br>
  Insert notes for this questions here.
  
  ````sql
  with customer_first_purchase as (
  select customers.id,
    min(customers.created_on) as creation_date,
    min(orders.purchase_ts) as first_purchase_date,
    date_diff(min(orders.purchase_ts), min(customers.created_on), day) as days_to_first_purchase
  from elist.customers
  left join elist.orders
    on customers.id = orders.customer_id
  group by customers.id
)

select round(avg(days_to_first_purchase), 2) as avg_days_to_first_purchase
from customer_first_purchase
  ````
</details>

<details>
<summary>Which marketing channels perform the best in each region? Does the top channel differ across regions?</summary> <br>
  Insert notes for this questions here.
  
  ````sql
  with marketing_channels_by_region as (
    select 
      geo_lookup.region,
      customers.marketing_channel,
      round(sum(orders.usd_price)) as total_sales,
      count(orders.usd_price) as order_count,
      round(avg(orders.usd_price), 2) as aov
    from elist.customers
    left join elist.orders
      on customers.id = orders.customer_id
    left join elist.geo_lookup
      on customers.country_code = geo_lookup.country
    group by customers.marketing_channel, geo_lookup.region
)

select *
from marketing_channels_by_region
order by region, total_sales desc, marketing_channel
  ````
</details>

<details>
<summary>For customers who purchased more than 4 orders across all years, what was the order ID, product, and purchase date of their most recent order?</summary> <br>
  Insert notes for this questions here.
  
  ````sql
  -- Breakdown by customers who made more than 4 orders across all years
  with repeat_customers as (
    select customer_id
    from elist.orders
    group by orders.customer_id
    having count(orders.id) > 4
  )
  
  -- The window function adds a column that ranks the recency of each order using purchase_ts
  -- this is partitioned by the customer_id, there are separate rankings for the rows of each customer_id
  select orders.customer_id,
    orders.id as order_id,
    orders.product_name,
    orders.purchase_ts,
    row_number() over (partition by orders.customer_id order by orders.purchase_ts desc) as order_ranking
  from elist.orders
  right join repeat_customers
     on orders.customer_id = repeat_customers.customer_id
  qualify row_number() over (partition by orders.customer_id order by orders.purchase_ts desc) = 1
  ````
</details>

<details>
<summary>For each brand, which month in 2020 had the highest number of refunds, and how many refunds did that month have?</summary> <br>
  Insert notes for this questions here.
  
  ````sql
  -- Lookup table for associated brands of products
  with brands as (
    select distinct product_name,
      case when lower(product_name) like '%apple%' or lower(product_name) like '%macbook%' then 'Apple'
  	    when lower(product_name) like '%thinkpad%' then 'Lenovo'
  	    when lower(product_name) like '%samsung%' then 'Samsung'
  	    when lower(product_name) like '%bose%' then 'Bose'
  	    else 'Unknown'
  	  end as brand_name,
    from elist.orders
  ),
  
  -- Calculating the refund count of each brand for each month of 2020
  monthly_refunds as ( 
    select date_trunc(orders.purchase_ts, month) as sales_month,
      brands.brand_name,
      count(order_status.refund_ts) as refund_count,
    from elist.orders
    left join elist.order_status
      on orders.id = order_status.id
    left join brands
      on orders.product_name = brands.product_name
    where orders.purchase_ts between '2020-01-01' and '2020-12-31'
    group by date_trunc(orders.purchase_ts, month), brands.brand_name
  )
  
  -- For each brand, select the month with the highest refund count
  select sales_month,
    brand_name,
    refund_count,
    row_number() over (partition by brand_name order by refund_count desc) as ranking
  from monthly_refunds
  qualify row_number() over (partition by brand_name order by refund_count desc) = 1 
  ````
</details>

