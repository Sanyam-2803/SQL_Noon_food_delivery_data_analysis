#  Noon 𝐅𝐨𝐨𝐝 𝐃𝐞𝐥𝐢𝐯𝐞𝐫𝐲 𝐃𝐚𝐭𝐚 𝐈𝐧𝐬𝐢𝐠𝐡𝐭𝐬  Project using SQL

Domain : Hospitality

📌 ℙ𝕣𝕠blem Statement

Food delivery Aggregator Noon food launched Food in Dubai on 1st Jan 2025.

Line Manager has assigned Jr Data Analyst to report key performance matrics to gauge the performance of the matrix. 

⚙️ Tools used 

Excel, MySQL Server & Canva

📌 𝔸𝕕𝕧𝕒𝕟𝕔𝕖𝕕 𝕊ℚ𝕃 𝕔𝕠𝕟𝕔𝕖𝕡𝕥𝕤

CTEs, window functions, Date & Time
functions, aggregation, filtering

📊 𝔻𝕒𝕥𝕒𝕤𝕖𝕥 𝕆𝕧𝕖𝕣𝕧𝕚𝕖𝕨

Orders table contains Order_ id, Customer_ code, Placed_ at, Restaurant_ id, Cuisine, Order_ status, Promo_ code_ Name.



![Food_Orders table](https://github.com/user-attachments/assets/05f25871-003e-49b2-b923-dba64d2d51f3)

🎯 𝕂𝕖𝕪 𝔹𝕦𝕤𝕚𝕟𝕖𝕤𝕤 𝕊ℚ𝕃 𝕢𝕦𝕖𝕣𝕚𝕖𝕤 / 𝕃𝕖𝕧𝕖𝕝-𝔸𝕕𝕧𝕒𝕟𝕔𝕖𝕕  


🔶 𝐓𝐨𝐩 2 𝐨𝐮𝐭𝐥𝐞𝐭𝐬 𝐛𝐲 𝐜𝐮𝐢𝐬𝐢𝐧𝐞 𝐭𝐲𝐩𝐞 𝐰𝐢𝐭𝐡𝐨𝐮𝐭 𝐮𝐬𝐢𝐧𝐠 𝐋𝐢𝐦𝐢𝐭 & 𝐓𝐨𝐩 𝐟𝐮𝐧𝐜𝐭𝐢𝐨𝐧


WITH cte as ( SELECT Restaurant_id,Cuisine,COUNT (*) as total_orders FROM orders
GROUP BY Restaurant_id,Cuisine )

SELECT * FROM ( SELECT *, row_number() OVER ( PARTITION BY Cuisine ORDER BY total_orders DESC ) as orders_rnk FROM cte ) A
WHERE orders_rnk < = 2 ;


![Orders12](https://github.com/user-attachments/assets/46d77a7c-cf24-46c4-a204-190cfb0e450f)

💡 Business Importance    

🎯 Enhanced Customer Experience    
📈 Data-Driven Marketing and Promotion    
💰 Revenue Optimization    


🔶  𝐃𝐚𝐢𝐥𝐲 𝐧𝐞𝐰 𝐜𝐮𝐬𝐭𝐨𝐦𝐞𝐫 𝐜𝐨𝐮𝐧𝐭 𝐟𝐫𝐨𝐦 𝐭𝐡𝐞 𝐥𝐚𝐮𝐧𝐜𝐡 𝐝𝐚𝐭𝐞 (𝐇𝐨𝐰 𝐦𝐚𝐧𝐲 𝐧𝐞𝐰 𝐜𝐮𝐬𝐭𝐨𝐦𝐞𝐫𝐬 𝐚𝐫𝐞 𝐰𝐞 𝐚𝐜𝐪𝐮𝐢𝐫𝐢𝐧𝐠 𝐞𝐯𝐞𝐫𝐲𝐝𝐚𝐲)

WITH new_customer as (SELECT Customer_code as new_customer,DATE(MIN(Placed_at)) as first_order_date FROM orders
GROUP BY Customer_code
ORDER BY  first_order_date asc)

SELECT first_order_date,COUNT(*) as no_new_customers FROM new_customer
GROUP BY first_order_date ;

![21](https://github.com/user-attachments/assets/9ca5ec0f-c666-4fbd-bf84-9dcab0589305)

💡 Business Importance  

📈 Core Indicator of Business Growth  
💰 Optimize Customer Acquisition Cost (CAC)  
🎯 Real-Time Marketing and Campaign Evaluation  


🔶 𝐂𝐨𝐮𝐧𝐭 𝐨𝐟 𝐚𝐥𝐥 𝐭𝐡𝐞 𝐮𝐬𝐞𝐫𝐬 𝐰𝐡𝐨 𝐰𝐞𝐫𝐞 𝐚𝐜𝐪𝐮𝐢𝐫𝐞𝐝 𝐢𝐧 𝐉𝐚𝐧 2025 𝐚𝐧𝐝 𝐨𝐧𝐥𝐲 𝐩𝐥𝐚𝐜𝐞𝐝 𝐨𝐧𝐞 𝐨𝐫𝐝𝐞𝐫 in Jan 2025 𝐨𝐫𝐝𝐞𝐫 𝐚𝐧𝐝 𝐝𝐢𝐝𝐧'𝐭 𝐩𝐥𝐚𝐜𝐞𝐝 𝐚𝐧𝐲 𝐨𝐭𝐡𝐞𝐫 𝐨𝐫𝐝𝐞𝐫  


SELECT Customer_code,Count(*)FROM orders
WHERE MONTH(Placed_at)=01 and YEAR(Placed_at)=2025 AND Customer_code NOT IN (SELECT DISTINCT Customer_code FROM orders
WHERE NOT month(Placed_at)= 01 AND YEAR(Placed_at)=2025
)
GROUP BY Customer_code 
HAVING COUNT(*)=1 ;


![31](https://github.com/user-attachments/assets/505cdbfa-51db-40ec-9ee0-bc4e76e8581c)

💡 Business Importance  






🔶 𝐋𝐢𝐬𝐭 𝐚𝐥𝐥 𝐭𝐡𝐞 𝐜𝐮𝐬𝐭𝐨𝐦𝐞𝐫𝐬 𝐰𝐢𝐭𝐡 𝐧𝐨 𝐨𝐫𝐝𝐞𝐫 𝐢𝐧 𝐭𝐡𝐞 𝐥𝐚𝐬𝐭 7 𝐝𝐚𝐲𝐬 𝐛𝐮𝐭 𝐰𝐞𝐫𝐞 𝐚𝐜𝐪𝐮𝐢𝐫𝐞𝐝 1 𝐦𝐨𝐧𝐭𝐡 𝐚𝐠𝐨 𝐰𝐢𝐭𝐡 𝐭𝐡𝐞𝐢𝐫 𝐟𝐢𝐫𝐬𝐭 𝐨𝐫𝐝𝐞𝐫𝐬 𝐨𝐧 𝐏𝐫𝐨𝐦𝐨


WITH cte as (SELECT Customer_code,MIN(Placed_at) as first_order_date,MAX(Placed_at) as latest_order_date FROM orders 
GROUP BY Customer_code)

SELECT cte.*,orders.Promo_code_Name as first_order_Promo_code FROM cte INNER JOIN orders ON cte.Customer_code = orders.Customer_code AND cte.first_order_date=orders.Placed_at 
WHERE DATE(latest_order_date)< CURDATE()-INTERVAL 7 DAY AND DATE(first_order_date)< CURDATE()-INTERVAL 30 DAY AND Promo_code_Name IS NOT NULL;


![32](https://github.com/user-attachments/assets/8c3ef447-1b01-4be8-b97a-92c7a502edd3)



🔶  𝐂𝐮𝐬𝐭𝐨𝐦𝐞𝐫𝐬 𝐰𝐡𝐨 𝐩𝐥𝐚𝐜𝐞𝐝 𝐦𝐨𝐫𝐞 𝐭𝐡𝐚𝐧 1 𝐨𝐫𝐝𝐞𝐫 𝐚𝐧𝐝 𝐚𝐥𝐥 𝐭𝐡𝐞𝐢𝐫 𝐨𝐫𝐝𝐞𝐫 𝐨𝐧 𝐏𝐫𝐨𝐦𝐨 𝐜𝐨𝐝𝐞

SELECT Customer_code,COUNT(*) as total_orders,COUNT(Promo_code_Name) as promo_orders 
FROM orders
GROUP BY Customer_code
HAVING COUNT(*)>1 and COUNT(*)= COUNT(Promo_code_Name) ;


![41](https://github.com/user-attachments/assets/22551916-bfa4-421e-b0e5-3f9b5293b82d)

🔶  𝐖𝐡𝐚𝐭 % 𝐨𝐟 𝐜𝐮𝐬𝐭𝐨𝐦𝐞𝐫𝐬 𝐰𝐞𝐫𝐞 𝐨𝐫𝐠𝐚𝐧𝐢𝐜𝐚𝐥𝐥𝐲 𝐚𝐜𝐪𝐮𝐢𝐫𝐞𝐝 𝐢𝐧 𝐉𝐚𝐧 2025 (𝐢.𝐞 𝐩𝐥𝐚𝐜𝐞𝐝 𝐭𝐡𝐞𝐢𝐫 𝐟𝐢𝐫𝐬𝐭 𝐨𝐫𝐝𝐞𝐫 𝐰𝐢𝐭𝐡𝐨𝐮𝐭 𝐩𝐫𝐨𝐦𝐨 𝐜𝐨𝐝𝐞)


WITH cte as (
SELECT *,row_number() over(PARTITION BY customer_code ORDER BY Placed_at ) as rw_no 
FROM orders 
WHERE MONTH(Placed_at)=01 
AND YEAR(Placed_at)=2025
)
SELECT ROUND(COUNT(CASE WHEN rw_no=1 AND Promo_code_Name IS NULL THEN Customer_code END)/COUNT(DISTINCT Customer_code)*100,1) as customers_acquired
FROM cte;


![50](https://github.com/user-attachments/assets/09bcc22b-aa07-414e-9d0b-1f6f3b5f6aa2)


🔶  𝐆𝐫𝐨𝐰𝐭𝐡 𝐓𝐞𝐚𝐦 𝐢𝐬 𝐩𝐥𝐚𝐧𝐧𝐢𝐧𝐠 𝐭𝐨 𝐜𝐫𝐞𝐚𝐭𝐞 𝐚 𝐭𝐫𝐢𝐠𝐠𝐞𝐫 𝐭𝐡𝐚𝐭 𝐰𝐢𝐥𝐥 𝐭𝐚𝐫𝐠𝐞𝐭 𝐜𝐮𝐬𝐭𝐨𝐦𝐞𝐫𝐬 𝐚𝐟𝐭𝐞𝐫 𝐭𝐡𝐞𝐢𝐫 𝐞𝐯𝐞𝐫𝐲 𝐭𝐡𝐢𝐫𝐝 𝐨𝐫𝐝𝐞𝐫 𝐰𝐢𝐭𝐡 𝐚 𝐩𝐞𝐫𝐬𝐨𝐧𝐚𝐥𝐢𝐳𝐞𝐝 𝐜𝐨𝐦𝐦𝐮𝐧𝐢𝐜𝐚𝐭𝐢𝐨𝐧 𝐚𝐧𝐝 𝐭𝐡𝐞𝐲 𝐚𝐬𝐤𝐞𝐝 𝐭𝐨 𝐜𝐫𝐞𝐚𝐭𝐞 𝐚 𝐪𝐮𝐞𝐫𝐲 𝐟𝐨𝐫 𝐭𝐡𝐢𝐬


WITH cte as (SELECT *,row_number() OVER(PARTITION BY Customer_code ORDER BY Placed_at) as order_no FROM orders)

SELECT * FROM cte
WHERE order_no%3=0 AND DATE(Placed_at)= CURRENT_DATE() ;

![100](https://github.com/user-attachments/assets/3cda7446-91f9-4ef0-ad98-4485196fe4df)


 






