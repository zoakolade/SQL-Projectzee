Answer the following questions and provide the SQL queries used to find the answer.

    
**Question 1: Which cities and countries have the highest level of transaction revenues on the site?**


SQL Queries: 
```sql
SELECT
city,
country,
MAX(totaltransactionrevenue / 1000000) AS max_products_ordered
FROM
all_sessions
GROUP BY
city, country
ORDER BY
max_products_ordered DESC NULLS LAST
LIMIT 5;
```



Answer:
"United States" 1015
"Israel" 602
"Australia" 358
"Canada" 82
"Switzerland" 16



**Question 2: What is the average number of products ordered from visitors in each city and country?**


SQL Queries:
```sql
SELECT
city,
country,
ROUND(AVG(orderedquantity), 2) AS average_products_ordered
FROM
all_sessions
JOIN
products USING (productsku)
GROUP BY
city, country
ORDER BY
average_products_ordered DESC
LIMIT 10;
```


Answer:
"Montenegro" 3786.00
"Mali" 3786.00
"Papua New Guinea" 2558.00
"Réunion" 2538.00
"Georgia" 2506.40
"Côte d’Ivoire" 1928.50
"Moldova" 1893.00
"Tanzania" 1429.00
"Trinidad & Tobago" 1379.50
"Armenia" 1351.00




**Question 3: Is there any pattern in the types (product categories) of products ordered from visitors in each city and country?**


SQL Queries:
```sql
SELECT
als.visitid,
p.name,
als.city,
als.country,
als.productrevenue,
COUNT(DISTINCT als.v2productcategory)
AS product_categories
FROM
all_sessions als
JOIN
products p ON p.productsku = als.productsku
WHERE
als.city != '(not set)' AND als.country != '(not set)'
GROUP BY
als.visitid, p.name, als.city, als.country, als.productrevenue
ORDER BY
als.country, als.city, product_categories DESC Nulls Last
LIMIT 10;
```



Answer:
"Albania" "Albania" 1
"Albania" "Albania" 1
"Albania" "Albania" 1
"Algeria" "Algeria" 1
"Algeria" "Algeria" 1
"Argentina" "Argentina" 1
"Argentina" "Argentina" 1
"Argentina" "Argentina" 1
"Argentina" "Argentina" 1
"Argentina" "Argentina" 1




**Question 4: What is the top-selling product from each city/country? Can we find any pattern worthy of noting in the products sold?**


SQL Queries:
```sql
WITH ProductSold AS (
SELECT
p.productsku,
p.name,
als.city,
als.country,
als.productrevenue,
MAX(als.totaltransactionrevenue) as totaltransactionrevenue
FROM
all_sessions als
JOIN products p ON p.productsku = als.productsku
GROUP BY
p.productsku,
p.name,
als.city,
als.country,
als.productrevenue,
als.totaltransactionrevenue
),
RankedProductSold AS (
SELECT
productsku,
name,
city,
country,
productrevenue,
totaltransactionrevenue,
RANK() OVER(PARTITION BY city, country ORDER BY totaltransactionrevenue DESC) AS rank
FROM ProductSold
)
SELECT
productsku,
name,
city,
country,
totaltransactionrevenue
FROM RankedProductSold
WHERE rank = 1
LIMIT 5;
```


Answer:
"GGOEYFKQ020699" " Custom Decals" "(not set)" "(not set)"
"GGOEGBMJ013399" "Sport Bag" "(not set)" "(not set)"
"GGOEGAAX0686" " Youth Short Sleeve Tee Red" "(not set)" "(not set)"
"GGOEGAAX0105" " Men's 100% Cotton Short Sleeve Hero Tee Black" "(not set)" "(not set)"
"GGOEGAAX0291" " Women's Short Sleeve Hero Tee Sky Blue" "(not set)" "(not set)"




**Question 5: Can we summarize the impact of revenue generated from each city/country?**

SQL Queries:
```sql
SELECT
city,
country,
SUM((productquantity * productprice)/1000000)
AS total_revenue
FROM
all_sessions
GROUP BY
city, country
ORDER BY
total_revenue DESC NULLS LAST
LIMIT 10;
```

Answer:
"United States" "United States" 5416
"Argentina" "Argentina" 99
"Ireland" "Ireland" 99
"Spain" "Spain" 89
"Canada" "Canada" 45
"France" "France" 17
"India" "India" 16
"Mexico" "Mexico" 16
"Colombia" "Colombia" 16
"Finland" "Finland" 1








