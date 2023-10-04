Hello! Currently a work in progress, transferring information OVER FROM BigQuery AND Tableau Desktop.

This is a complementary portion to the [Nexus Sales Analysis](https://github.com/aduong58/portfolio_projects/tree/main/Nexus-Sales-Analysis) project. This subsegment of the main project will contain:
1. SQL queries that were used for ad-hoc analysis before AND during the Excel analysis.
2. Tableau dashboard created towards the END of the project for more visual analysis of the data.


## Ad-hoc Analysis using SQL
<details>
<summary>What are the monthly AND quarterly sales trends for Macbooks sold in North America across all years </summary> <br>
  Insert notes for this questions here.
  
  ````sql
  WITH quarterly_data AS (
    SELECT date_trunc(orders.purchase_ts, quarter) AS purchase_quarter,
      geo_lookup.region,
      ROUND(SUM(orders.usd_price)) AS quarterly_sales,
      COUNT(orders.usd_price) AS order_count,
      ROUND(AVG(orders.usd_price)) AS aov
    FROM elist.orders
    INNER JOIN elist.customers
     ON customers.id = orders.customer_id
    LEFT JOIN elist.geo_lookup
     ON customers.country_code = geo_lookup.country
    WHERE LOWER(orders.product_name) LIKE "%macbook%"
      AND LOWER(geo_lookup.region) LIKE "%na%"
    GROUP BY purchase_quarter, geo_lookup.region
    ORDER BY purchase_quarter DESC
  )
  
  SELECT ROUND(AVG(quarterly_sales)) AS average_quarterly_sales,
    AVG(order_count) AS avg_order_count,
    AVG(aov) AS avg_aov
  FROM quarterly_data
  ```` 
</details>

<details>
<summary>What was the monthly refund rate for purchases made in 2020? How many refunds did we have each month in 2021 for Apple products?</summary> <br>
  Insert notes for this questions here.
  
  ````sql
  WITH refund_rates_2020 AS (
    SELECT date_trunc(orders.purchase_ts, month) AS sales_month, 
      ROUND(COUNT(order_status.refund_ts) / COUNT(*), 4) AS refund_rate
    FROM elist.orders
    LEFT JOIN elist.order_status
     ON orders.id = order_status.id
    WHERE extract(year FROM orders.purchase_ts) = 2020
    GROUP BY sales_month
    ORDER BY sales_month
  ),
  
  apple_refunds_2021 AS (
    SELECT date_trunc(orders.purchase_ts, month) AS sales_month,
      COUNT(order_status.refund_ts) AS refunds_count
    FROM elist.orders
    LEFT JOIN elist.order_status
     ON orders.id = order_status.id
    WHERE extract(YEAR FROM orders.purchase_ts) = 2021
      AND (LOWER(orders.product_name) LIKE "%apple%" 
      OR LOWER(orders.product_name) LIKE "%macbook%")
    GROUP BY sales_month
    ORDER BY sales_month
  )
  
  SELECT * FROM apple_refunds_2021
  ````
</details>

<details>
<summary>Are there certain products that are getting refunded more frequently than others? What are the top 3 most frequently refunded products across all years? What are the top 3 products that have the highest count of refunds?</summary> <br>
  Insert notes for this questions here.
  
  ````sql
  SELECT 
    CASE WHEN orders.product_name LIKE "%\"\"%" THEN "27in 4K gaming monitor"
      ELSE orders.product_name
      END AS product_name_clean,
    COUNT(order_status.refund_ts) AS refund_count,
    ROUND(COUNT(order_status.refund_ts) / COUNT(*), 4) AS refund_rate
  FROM elist.orders
  LEFT JOIN elist.order_status
   ON orders.id = order_status.id
  GROUP BY product_name_clean
  ORDER BY refund_rate DESC
  -- ORDER BY refund_count DESC
  ````
</details>

<details>
<summary>What’s the average order value across different account creation methods in the first two months of 2022? Which method had the most new customers in this time?</summary> <br>
  Insert notes for this questions here.
  
  ````sql
  SELECT 
    CASE WHEN customers.account_creation_method is null then "unknown"
      ELSE customers.account_creation_method
      END AS account_creation_method_clean,
    ROUND(AVG(orders.usd_price), 2) AS aov,
    COUNT(*) AS new_customer_count
  FROM elist.orders
  LEFT JOIN elist.customers
   ON orders.customer_id = customers.id
  WHERE customers.created_on between '2022-01-01' AND '2022-02-28'
  GROUP BY account_creation_method_clean
  ORDER BY aov DESC
  ````
</details>

<details>
<summary>What’s the average time between customer registration AND placing an order?</summary> <br>
  Insert notes for this questions here.
  
  ````sql
  WITH customer_first_purchase AS (
    SELECT customers.id,
      MIN(customers.created_on) AS creation_date,
      MIN(orders.purchase_ts) AS first_purchase_date,
      DATE_DIFF(MIN(orders.purchase_ts), MIN(customers.created_on), day) AS days_to_first_purchase
    FROM elist.customers
    LEFT JOIN elist.orders
     ON customers.id = orders.customer_id
    GROUP BY customers.id
)

  SELECT ROUND(AVG(days_to_first_purchase), 2) AS avg_days_to_first_purchase
  FROM customer_first_purchase
  ````
</details>

<details>
<summary>Which marketing channels perform the best in each region? Does the top channel differ across regions?</summary> <br>
  Insert notes for this questions here.
  
  ````sql
  WITH marketing_channels_by_region AS (
    SELECT 
      geo_lookup.region,
      customers.marketing_channel,
      ROUND(SUM(orders.usd_price)) AS total_sales,
      COUNT(orders.usd_price) AS order_count,
      ROUND(AVG(orders.usd_price), 2) AS aov
    FROM elist.customers
    LEFT JOIN elist.orders
     ON customers.id = orders.customer_id
    LEFT JOIN elist.geo_lookup
     ON customers.country_code = geo_lookup.country
    GROUP BY customers.marketing_channel, geo_lookup.region
)

SELECT *
FROM marketing_channels_by_region
ORDER BY region, total_sales DESC, marketing_channel
  ````
</details>

<details>
<summary>For customers who purchased more than 4 orders across all years, what was the order ID, product, AND purchase date of their most recent order?</summary> <br>
  Insert notes for this questions here.
  
  ````sql
  -- Breakdown by customers who made more than 4 orders across all years
  WITH repeat_customers AS (
    SELECT customer_id
    FROM elist.orders
    GROUP BY orders.customer_id
    having COUNT(orders.id) > 4
  )
  
  -- The window function adds a column that ranks the recency of each order using purchase_ts
  -- this is partitioned by the customer_id, there are separate rankings for the rows of each customer_id
  SELECT orders.customer_id,
    orders.id AS order_id,
    orders.product_name,
    orders.purchase_ts,
    ROW_NUMBER() OVER (PARTITION BY orders.customer_id ORDER BY orders.purchase_ts DESC) AS order_ranking
  FROM elist.orders
  RIGHT JOIN repeat_customers
    ON orders.customer_id = repeat_customers.customer_id
  QUALIFY ROW_NUMBER() OVER (PARTITION BY orders.customer_id ORDER BY orders.purchase_ts DESC) = 1
  ````
</details>

<details>
<summary>For each brand, which month in 2020 had the highest number of refunds, AND how many refunds did that month have?</summary> <br>
  Insert notes for this questions here.
  
  ````sql
  -- Lookup table for associated brands of products
  WITH brands AS (
    SELECT distinct product_name,
      CASE
        WHEN LOWER(product_name) LIKE '%apple%' OR LOWER(product_name) LIKE '%macbook%' then 'Apple'
        WHEN LOWER(product_name) LIKE '%thinkpad%' then 'Lenovo'
        WHEN LOWER(product_name) LIKE '%samsung%' then 'Samsung'
        WHEN LOWER(product_name) LIKE '%bose%' then 'Bose'
        ELSE 'Unknown'
      END AS brand_name
    FROM elist.orders
  ),
  
  -- Calculating the refund count of each brand for each month of 2020
  monthly_refunds AS ( 
    SELECT date_trunc(orders.purchase_ts, month) AS sales_month,
      brands.brand_name,
      COUNT(order_status.refund_ts) AS refund_count
    FROM elist.orders
    LEFT JOIN elist.order_status
     ON orders.id = order_status.id
    LEFT JOIN brands
     ON orders.product_name = brands.product_name
    WHERE orders.purchase_ts between '2020-01-01' AND '2020-12-31'
    GROUP BY date_trunc(orders.purchase_ts, month), brands.brand_name
  )
  
  -- For each brand, SELECT the month WITH the highest refund count
  SELECT sales_month,
    brand_name,
    refund_count,
    ROW_NUMBER() OVER (PARTITION BY brand_name ORDER BY refund_count DESC) AS ranking
  FROM monthly_refunds
  QUALIFY ROW_NUMBER() OVER (PARTITION BY brand_name ORDER BY refund_count DESC) = 1 
  ````
</details>

