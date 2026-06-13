PROJECT OVERVIEW 

 The goal of this analysis is to evaluate sales performance, customer behavior, and product trends to identify opportunities for revenue growth and improved decision-making. 

 The dataset contains customer transactions including demographics, purchase amounts, product categories, payment methods, and customer ratings. 

 
BUSINESS QUESTIONS 

 
1.	How does seasonality impact overall revenue performance across the business? 

2.    How do different product categories contribute to overall revenue, and which categories drive the most value? 

3.    Which individual products are driving revenue, and how concentrated is performance across top and bottom items? 

4.    How do customer demographics influence purchasing behavior and revenue generation? 

5.   What patterns exist in customer purchasing behavior, and are customers returning or primarily one-time buyers? 

6.   How do product ratings vary across categories, and what do they indicate about customer satisfaction? 

 

We will explore insights such as: 

🔹 Revenue by Category 

🔹 Top Performing Products 

🔹 Customer Demographics 

🔹 Customer Retention 

🔹 Product Ratings 

 

We will use these insights to make business recommendations with the purpose of increasing revenue and customer satisfaction. 

 

 
SEASONAL REVENUE ANALYSIS 

 How does seasonality impact overall revenue performance across the business? 

 

SELECT season, SUM(amount) AS total_sales 

FROM store1 

GROUP BY season 

ORDER BY total_sales DESC; 

 

 Revenue is relatively consistent across all seasons, with no significant seasonal spikes or drops. 

 

Business Recommendation:  

The business may benefit from targeted seasonal promotions to create stronger revenue peaks and maximize sales during specific periods. 

DEPARTMENT PERFORMANCE 

 

How do different product categories contribute to overall revenue, and which categories drive the most value? 

 

SELECT category, SUM(AMOUNT) as department_sales FROM STORE1 

GROUP BY category 

ORDER BY department_sales DESC; 

 

 

 

Electronics is the dominant revenue-generating category, significantly outperforming all other departments. 

 

Business Recommendations: 

The business should prioritize investment in Electronics while analyzing underperforming departments to identify opportunities for improvement. 

The business should also investigate WHY Electronics dominate. Is it due to: 

Higher prices? 

More transactions? 

Customer preference? 

The answer to these questions will provide guidance on how to move forward to drive sales and opportunities. 

 

Let’s Dive A Little Deeper: 

 

Department Sales By Season 

SELECT category, season, SUM(amount) as revenue from store1 

GROUP BY season, category 

ORDER BY category, revenue desc; 

 

 

 

Key Insights: 

 

• Electronics is the dominant revenue driver across all seasons, with peak performance in Spring. 

 

• Footwear is a strong secondary category, showing its highest performance in Spring, indicating potential for growth. 

 

• Sports category performs best in Winter, suggesting seasonal demand tied to specific activities. 

 

• Women’s Clothing shows consistent performance, with slightly higher sales in Spring and Winter. 

 

• Men’s Clothing performs evenly in Summer and Winter, indicating less seasonality. 

 

• Accessories and Groceries remain stable year-round, indicating consistent demand. 

 

• Home category sees increased sales in Spring, suggesting seasonal purchasing behavior. 

 

• Beauty products experience a decline in Summer compared to other seasons. 

 

 

Business Recommendations: 

 

• Prioritize Electronics during Spring through increased inventory and targeted promotions to maximize peak performance. 

 

• Expand marketing efforts for Footwear, particularly in Spring, to capitalize on its strong seasonal demand. 

 

• Increase focus on Sports products during Winter to align with peak seasonal interest. 

 

• Maintain consistent inventory levels for Accessories and Groceries due to stable demand patterns. 

 

• Investigate the decline in Beauty sales during Summer and explore promotional strategies to improve performance. 

 

• Leverage Spring demand for Home products through seasonal campaigns and product bundling. 

  

 

PRODUCT PERFORMANCE 

 

Which individual products are driving revenue, and how concentrated is performance across top and bottom items? 

select itempurchased, sum(amount) as revenue from store1 

group by itempurchased 

order by revenue desc; 

 

 

 

The top-performing products are all Electronics (Laptop, Mobile Phone, Headphones, Smart Watch), reinforcing that Electronics is the primary revenue driver.  

 

Conversely, the lowest-performing products are grocery-related items, aligning with earlier findings that Groceries generate the least revenue overall. 

 

Business Recommendations: 

Increase focus on top-performing Electronics products through targeted marketing, bundling strategies, and inventory prioritization to maximize revenue from proven demand drivers 

Evaluate profit margins across all products, as high revenue does not necessarily indicate high profitability. Ensure top-performing products are also delivering strong margins. 

Assess whether low-performing grocery items should be improved through pricing, promotions, or repositioning, rather than immediately eliminated. 

Identify whether low-performing products contribute to customer retention or cross-selling opportunities before making decisions to reduce or remove them. 

 

Important Observation: 

The concentration of revenue in a small number of products suggests potential dependency risk on Electronics. Diversifying revenue streams by strengthening mid-tier products could reduce reliance on a single category. 

 

CUSTOMER DEMOGRAPHICS 

 

How do customer demographics influence purchasing behavior and revenue generation? 

 Let’s discover how men and women contribute to revenue: 

SELECT gender, sum(amount) as revenue 

FROM store1 

GROUP BY gender; 

 

Male customers generate significantly more revenue than female customers, contributing over four times the total revenue. 

 

Further analysis should determine whether this difference is driven by customer volume or spending behavior to identify opportunities for targeted marketing and growth. 

 

Let’s Dive a Little Deeper... 

How do genders perform based on category? 

 

 

 

Male customers primarily drive revenue through Electronics, followed by Sports and Footwear, indicating a strong preference for high-value and performance-related products. 

 

Female customers show a more balanced distribution, with Footwear, Women’s Clothing, and Accessories contributing most to revenue. 

 

Business Recommendations: 

Evaluate profit margins for Sports and Footwear categories to determine whether increased marketing investment could yield higher overall profitability compared to Electronics. 

Footwear performs strongly across both male and female customers, indicating it may be an underutilized growth category that could benefit from increased marketing and inventory focus. 

Develop targeted marketing strategies based on gender-specific purchasing behavior, emphasizing Electronics and Sports for male customers, and Footwear and Apparel for female customers. 

Analyze the overlap between Accessories and Beauty products to identify bundling or cross-selling opportunities  

 

Important Observation: 

The concentration of male spending in a few categories may present both an opportunity for targeted growth and a risk of over-reliance on specific product segments. 

 

CUSTOMER RETENTION 

 

What patterns exist in customer purchasing behavior, and are customers returning or primarily one-time buyers? 

Let’s explore how many of our customers have made previous purchases: 

SELECT 

COUNT(DISTINCT customerid) AS total_customers, 

COUNT(DISTINCT CASE WHEN previouspurchases > 0 THEN customerid END) AS returning_customers 

FROM store1; 

 

4967 out of 5000 customers are repeat customers 

 

Let’s break it down by department: 

Which categories retain customers the best? 

 

SELECT 

category, 

COUNT(DISTINCT customerid) AS total_customers, 

COUNT(DISTINCT CASE WHEN previouspurchases > 0 THEN customerid END) AS returning_customers 

FROM store1 

GROUP BY category; 

 

A significant portion of customers are repeat buyers, indicating strong customer retention and ongoing engagement with the business. 

Business Recommendations: 

• Implement loyalty programs to further encourage repeat purchases 

 

PRODUCT RATINGS 

 

How do product ratings vary across categories, and what do they indicate about customer satisfaction? 

 

Let’s explore average rating per department: 

 

select category, avg(itemrating) as avg_rating 

from store1 

group by category 

order by avg_rating desc; 

 

The data shows no significant difference in ratings across departments, each department having an average rating above 3.5.  

 

How about categories with the most ratings below 3? 

SELECT 

category, 

COUNT(CASE WHEN itemrating < 3 THEN 1 END) AS low_ratings 

FROM store1 

GROUP BY category; 

 

 

Footwear is a top revenue-generating category, but it also has the highest number of low customer ratings, indicating a potential trade-off between sales volume and customer satisfaction. 

 

Business Recommendations: 

 

• Investigate why footwear has high low ratings (quality, sizing, comfort, returns) 

• Analyze specific products within footwear to identify problem items 

• Consider supplier/vendor review if quality issues are consistent 

• Improve product descriptions or sizing guides to reduce mismatched expectations 

• Monitor footwear ratings over time to ensure improvements are effective 

 

While footwear is a strong revenue driver, improving customer satisfaction in this category presents an opportunity to increase repeat purchases and long-term customer value. 
