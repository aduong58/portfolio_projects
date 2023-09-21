# Project - Nexus Sales Analysis
Founded in 2018, Nexus is an e-commerce company that sells popular electronics products and has since expanded to a global customer base. 

In this data analysis project, I examined key metrics within sales data to draw out insights on the overall performance of Nexus and provide data-driven recommendations in the areas of sales, product, marketing, and operations.


The main metrics I focused on were sales revenue, average order value (AOV), and order counts. I worked with these metrics to analyze and break down overall sales trends, product performance, effectiveness of their loyalty program, as well as other relevant areas of the business. <br>

# About the data
The company maintains a [core dataset](https://github.com/aduong58/portfolio_projects/blob/main/Nexus-Sales-Analysis/nexus_original_dataset.png) consisting of orders, customers, products, and geographic information. 
<img src="https://github.com/aduong58/portfolio_projects/assets/58454640/423c131b-b605-4921-af29-fa584290e955" width=80% height=80%>

Documentation on the cleaning and preparation of the data can be found [**here**](https://github.com/aduong58/portfolio_projects/blob/main/Nexus-Sales-Analysis/Nexus%Cleaning%Documentation.pdf)

The workbook containing the original dataset and created tables can be found **here**


# Technical Analysis
The analysis portion of this project was done within Excel. To summarize insights and segment the data into different categories, I chose to use pivot tables alongside conditional formatting. Throughout the project, I utilized aggregation functions to clean the data and calculate new fields.

**Overall Sales Trends**
Revenue Growth             |  AOV and Order Count      |
:-------------------------:|:-------------------------:|
![revenue_by_quarter](https://github.com/aduong58/portfolio_projects/assets/58454640/c43aaf7a-79c8-45b6-b64e-3be0ddf0809d)  |  ![aov_orders_by_year](https://github.com/aduong58/portfolio_projects/assets/58454640/dbc62318-053f-4154-9dcf-3c5a6097f125) |
Cells conditionally formatted on revenue growth rate percentage. | Cells conditionally formatted on AOV and order count columns.


In 2019, the initial year of sales records, Nexus generated $3.26 million in sales. In the following year, the company observed significant growth, generating $8.62 million in sales for 2020, more than doubling the revenue of the previous year's sales.

Analyzing the quarterly breakdown of revenue data reveals a peak in Q2 of 2020, where sales generated $2.5 million for just that quarter. Following the period of substantial growth in 2020, there is a gradual decrease in revenue generated from sales. 

This trend extends to other key metrics. Nexus saw its peak order count at 30.7K in 2021, followed by a steady decline in 2022. Average Order Value (AOV) mirrored the revenue pattern a bit more cloesly, reaching its highest point at $310 in Q4 2020 and gradually declining to $230 in 2022.
<br><br>

Revenue and Order Count by Region|
:-------------------------:|
![image](https://github.com/aduong58/portfolio_projects/assets/58454640/64afc715-b6c5-4535-8c6a-4aa855fc4e08)|

North America leads as Nexus's primary customer market, contributing over 50% of total revenue and orders, driving $12.5 million in revenue and 48,000 orders. This is followed by the Europe, Middle East, and Africa region, contributing to just under 30% of both revenue and orders.

While ranking third in terms of total revenue, the Asia-Pacific region demonstrates the highest spending per order with an AOV of $275, the only region to surpass the overall average of $259.
<br><br>

**Product Performance**
Product Orders             |  Product Revenue          |
:-------------------------:|:-------------------------:|
![product_orders](https://github.com/aduong58/portfolio_projects/assets/58454640/8feebc5d-0f74-4fa1-b7c6-b1c1a0c4ceb0)  |  ![product_sales](https://github.com/aduong58/portfolio_projects/assets/58454640/e3dc502d-2199-4355-ad5a-185759e8184b) 

Looking at the order count of products sold by Nexus, the top performing product is Apple Airpods Headphones, making up nearly 45% of all orders made. On the other hand, the worst-performing product sold was the Bose Soundsport Headphones, making up just 0.03% of all orders made through Nexus.

The second most popular product sold by Nexus is the 4K Gaming Monitor, making up 22% of orders made. It has also generated the most revenue of all products at $8.4M, making up 35% of the total revenue generated from sales. <br><br>


**Loyalty Program**
Sales, AOV, and Orders by Loyalty Membership|
:-------------------------:|
![loyalty program](https://github.com/aduong58/portfolio_projects/assets/58454640/5a3094df-cda4-4638-8c8b-dd23a3813075)
Quarters are highlighted where sales, AOV, and order count perform better in either group (Loyalty vs. Non-Loyalty) |  

In the early years of the loyalty program, the program was not performing as well as the orders made by regular customers. However, in more recent years, sales generated from members of the loyalty program have outpaced that of regular customers in various metrics.

In 2021 and beyond, members of the loyalty program placed 16% more orders and generated over $1M more in revenue than non-loyalty customers. In 2022, loyalty members spent more money per order with an AOV of $246 compared to the AOV of regular customers at $212. <br><br>

**Purchase Platform and Marketing Channels**
Orders by Purchase Platform| Revenue by Marketing Channel          |
:-------------------------:|:-------------------------:|
![purchase_platform](https://github.com/aduong58/portfolio_projects/assets/58454640/612249ec-15f8-43b9-98bd-92cd930ce5f4) | ![marketing channel](https://github.com/aduong58/portfolio_projects/assets/58454640/407d5e45-2ba6-4a14-b585-51be0e3501ef)
Quarterly order counts are conditionally formatted by each individual purchase platform column.  | Quarterly revenues are conditionally formatted by each individual marketing channel column

The main purchase platform for orders continues to be our desktop website, accounting for 94% of orders. However, in more recent years (2021 and 2022), there has been a significant growth in orders made through the mobile app.

Direct marketing is shown to be the top marketing channel for Nexus, accounting for roughly 82% of total revenue. There appears to be some deviating behavior between channels. Email marketing experiences a revenue peak in 2021, slightly later than the other channels. Additionally, in 2022, there is a surge in revenue from orders where the marketing channel is not known.

# Recommendations

**Overall Sales**
- In response to the recent decline in sales, I would recommend working to identify our core customer base (loyalty members & top regional markets) and investing in efforts to retain that segment of customers.
  
**Product Performance**
- Invest more in products that have historically generated the most revenue and orders (Apple Airpods & 4K Gaming Monitors) for Nexus.
- Consider discontinuing low-performance products like the Bose SoundSport Headphones to streamline product offerings.

**Loyalty Program**
- Given the growth and performance of Nexus' loyalty program in recent years, I would recommend maintaining it and taking a closer look at what has been drawing customers to the program.
- Things to consider are loyalty program awareness, associated incentives of being a member, as well as the alignment of the program with the overall business goals of Nexus.

**Purchase Platform and Marketing Channels**
- In more recent years the mobile site has been growing as a purchase platform, I would recommend reviewing the mobile site operations to maintain and possibly expand ease of usability.
- Further analyze revenue data in conjunction with marketing activities data to see if there are correlations in behavior between the two.
# Additional Notes
- A [surge in e-commerce sales](https://www.census.gov/library/stories/2022/04/ecommerce-sales-surged-during-pandemic.html) during the COVID-19 pandemic could be a large factor in the initial spike of sales. The recent decline in sales may reflect a shift as the business aligns with its true consumer base.
- With additional product cost data, we can enhance our analysis by assessing profitability, providing deeper insights into product line performance


