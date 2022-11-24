#### Some SQL practice interview questions which I attempted

## [Data Lemur 🐒](https://datalemur.com/)
### Level: Easy
#### ✔️ Data Science Skills | LinkedIn <br>
Given a table of candidates and their skills, find the candidates best suited for an open Data Science job. Write a query to list the candidates who are proficient in Python, Tableau, and PostgreSQL. Sort the the output by candidate ID in ascending order.
```sql
SELECT DISTINCT candidate_id 
FROM candidates
WHERE skill IN ('Python', 'Tableau', 'PostgreSQL')
GROUP BY candidate_id
HAVING COUNT(skill)=3
ORDER BY candidate_id
```
![image](https://user-images.githubusercontent.com/40571742/203689944-053ca33e-25a3-4389-9257-a6ee5b03ecf6.png)

#### ✔️ Page With No Likes | Facebook/Meta <br>
Given tables about Facebook pages and page likes. Write a query to return the page IDs of all the Facebook pages that don't have any likes. The output should be in ascending order.
```sql
SELECT pages.page_id
FROM pages
LEFT JOIN page_likes ON pages.page_id = page_likes.page_id
WHERE user_id IS NULL
ORDER BY pages.page_id
```
![image](https://user-images.githubusercontent.com/40571742/203690266-f21097c2-a1d5-44bc-879c-e4ce7daaa2ac.png)

#### ✔️ Laptop vs. Mobile Viewership | New York Times <br>
Given the table containing information on viewership by device type - laptop, tablet, and phone. Define “mobile” as the sum of tablet and phone viewership numbers. Write a query to compare the viewership on laptops versus mobile devices. <br>
Output the total viewership for laptop and mobile devices in the format of "laptop_views" and "mobile_views".
```sql
SELECT 
  SUM(CASE WHEN device_type = ('laptop') THEN 1 ELSE 0 END) AS laptop_views,
  SUM(CASE WHEN device_type IN ('tablet', 'phone') THEN 1 ELSE 0 END) AS mobile_views
FROM viewership
```
![image](https://user-images.githubusercontent.com/40571742/203690692-600c196b-ac0b-453d-b5c3-d71b2d4b8ac7.png)

#### ✔️ Average Review Ratings | Amazon <br>
Given the reviews table, write a query to get the average stars for each product every month.
The output should include the month in numerical value, product id, and average star rating rounded to two decimal places. Sort the output based on month followed by the product id.
```sql
SELECT 
  extract(month from submit_date) AS mth,
  product_id AS product,
  ROUND(AVG(stars),2) AS avg_stars
FROM reviews
GROUP BY extract(month from submit_date), product
ORDER BY mth, product
```
![image](https://user-images.githubusercontent.com/40571742/203690884-3ae429a6-8beb-412e-ac89-ac22ff968d54.png)

#### ✔️ Cities With Completed Trades | Robinhood
Given the tables containing information on Robinhood trades and users. Write a query to list the top three cities that have the most completed trade orders in descending order.
```sql
SELECT city, 
  SUM(CASE WHEN status = 'Completed' THEN 1 ELSE 0 END) AS total_orders
FROM trades JOIN users
ON trades.user_id = users.user_id
GROUP BY city
ORDER BY total_orders DESC
LIMIT 3
```
![image](https://user-images.githubusercontent.com/40571742/203691191-772fb685-d561-4228-9d86-8377e544e13d.png)
