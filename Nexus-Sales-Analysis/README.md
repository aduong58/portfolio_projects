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
The analysis portion of this project was done within Excel. To summarize insights and segment the data into different categories, I chose to use pivot tables alongside conditional formatting. Throughout the project I utilized aggregation functions to clean the data and calculate new fields.

**Overall Sales Trends**
Total Sales                |  AOV and Orders           | Sales by Month
:-------------------------:|:-------------------------:|:-------------------------:
![sales_by_year](https://github.com/aduong58/portfolio_projects/assets/58454640/d2b7c9b6-3f8e-4533-9e65-d8a725d675d8)  |  ![aov_orders_by_year](https://github.com/aduong58/portfolio_projects/assets/58454640/37010556-d25e-4197-8711-2817d37b4def) | ![sales_by_month](https://github.com/aduong58/portfolio_projects/assets/58454640/187f8f2d-20d2-40b8-b6bf-83b28671a29d)

In 2019, the initial year of sales records, Nexus generated $3.26 million in sales. In the following year, the company observed a significant growth in revenue, generating $8.62 million in sales for 2020, more than doubling the revenue of the previous year's sales.

Analyzing the quarterly breakdown of revenue data reveals a peak in Q4 of 2020, where sales generated $2.5 million for just that quarter. Following this period of substantial growth, there has been a gradual decrease in revenue generated from sales. <br><br>


**Product Performance**
Product Orders             |  Product Revenue          |
:-------------------------:|:-------------------------:|
![product_orders](https://github.com/aduong58/portfolio_projects/assets/58454640/6645e614-967a-46e3-a1b1-9d7e6aee1052)  |  ![product_sales](https://github.com/aduong58/portfolio_projects/assets/58454640/e3dc502d-2199-4355-ad5a-185759e8184b) 

Looking at the order count of products sold by Nexus, the top performing product is Apple Airpods Headphones, making up nearly 45% of all orders made. On the other hand, the worst performing product sold was the Bose Soundsport Headphones, making up just .03% of all orders made through Nexus.

Another product of interest is the 4k Gaming Monitor. It is the second most popular product sold by Nexus, making up 22% of orders made. It has also generated the most revenue of all products at $8.4M, making up 35% of the total revenue generated from sales. <br><br>


**Loyalty Program**
Sales, AOV, and Orders by Loyalty Membership|
:-------------------------:|
![loyalty_program](https://github.com/aduong58/portfolio_projects/assets/58454640/73b8ea18-2cb8-490a-a426-22c37056fd07)  
Quarters are highlighted where sales, AOV, and order count perform better in either group (Loyalty vs. Non-Loyalty) |  

In the early years of the loyalty program, the program was not performing as well as the orders made by regular customers. However, in more recent years, sales generated from members of the loyalty program have begun to outpace that of regular customers in various metrics.

In 2021 and beyond, members of the loyalty program placed 16% more orders and generated over $1M more in revenue than non-loyalty customers. In addition to this, in 2022, loyalty members spent more money per order with an AOV of $246 compared to the AOV of regular customers at $212. <br><br>

**Purchase Platform and Marketing Channels**
Orders by Purchase Platform|  Orders, Revenue, and AOV by Marketing Channel          |
:-------------------------:|:-------------------------:|
![purchase_platform](https://github.com/aduong58/portfolio_projects/assets/58454640/612249ec-15f8-43b9-98bd-92cd930ce5f4) | <img src="https://github.com/aduong58/portfolio_projects/assets/58454640/14acab13-1902-4672-9f6c-5f8ccc96d7b4" width=95% height=65%> 
Quarters are conditionally formatted on the order count of each purchase platform.  | Marketing channels with order count, revenue, and AOV metrics.

The main purchase platform for orders continues to be our desktop website accounting for 94% of orders. However, in more recent years (2021 and 2022), there has been a significant growth in orders made through the mobile app.


# Recommendations

**Overall Sales**
- In response to the recent decline in sales, I would recommend working to identify our core customer base and focusing efforts to retain that segment of customers. Looking at the loyalty program could be a good direction to start.

**Product Performance**
- I would recommend investing more in products that have historically generated the most revenue and orders (Apple Airpods & 4K Gaming Monitors) for Nexus.
- I also would consider discontinuing low performance products like the Bose SoundSport Headphones to streamline product offerings.

**Loyalty Program**
- Seeing the growth and performance of Nexus' loyalty program within the recent years of sales, I would recommend keeping the loyalty program and taking a closer look at what has been drawing customers to the program.
- Things to consider are the awareness/marketing of the loyalty program, associated incentives of being a member, as well as alignment of the loyalty program with the overall business goals of Nexus.

**Purchase Platform and Marketing Channels**
- In more recent years the mobile site has been growing as a purchase platform, I would recommend reviewing the mobile site operations to maintain and possibly expand ease of usability.
# Additional Notes
- Covid technology sales could be a factor in initial sales highs -> recent years of sales tapering into true sales
- Given more data on product costs, we would be able to add profitability to our analysis and better understand the overall performance of different products.


