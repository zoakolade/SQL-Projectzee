What are your risk areas? Identify and describe them.

I. Data Loss: Deleting or altering data without proper backups can result in irreversible damage therefore while importing the data I did not delete or alter any of the details provided. I created the tables then imported the csv.files without altering any detail

II. Data Integrity: Enforcing data integrity constraints like primary keys and foreign keys help maintain data quality. Therefore PK and FK was defined for the dimension and fact table.

III. Data Type Conversion: Incorrectly converting data types can lead to loss of precision or unexpected results therefore I needed to look into the data and determine what the correct data type should be and write the appropriate query for conversion.

IV. Null Values: The data contains a lot of Null values which if not properly handled can skew analysis and lead to incorrect conclusions. In the sale_report table where column is ratio there lots of NULL when cleaned

V. Join Operations: Using inappropriate join conditions can lead to incorrect or incomplete results. Therefore I used subqueries where possible to double my results.

Describe your QA process and include the SQL queries used to execute it.

QA Process was used to check the completeness, uniqueness and consistency of the data. To check for the completeness I used the COUNT in my query to confirm if there is any missing data from the entire data and which column has a NULL value. I used DISTINCT function to further drill down to the unique values in the data. For the consistency I ran a corrected query on for date and time columns where the initial data was presented as an integer and not a datetime function.

SELECT
COUNT(*) AS total_rows,
COUNT(productsku) AS column1_nulls,
COUNT(name) AS column2_nulls,
COUNT(orderedQuantity) AS column3_nulls,
COUNT(stockLevel) AS column4_nulls,
COUNT(restockingLeadTime) AS column5_nulls,
COUNT(sentimentScore) AS column6_nulls,
COUNT(sentimentMagnitude) AS column7_nulls
FROM products;

SELECT
COUNT(*) AS total_rows,
COUNT(DISTINCT productSKU) AS column1_nulls,
COUNT(DISTINCT total_ordered) AS column2_nulls,
COUNT(DISTINCT name) AS column3_nulls,
COUNT(DISTINCT stockLevel) AS column4_nulls,
COUNT(DISTINCT restockingLeadTime) AS column5_nulls,
COUNT(DISTINCT sentimentScore) AS column6_nulls,
COUNT(DISTINCT sentimentMagnitude) AS column7_nulls,
COUNT(DISTINCT ratio) AS column8_nulls
FROM sales_report;
QA Process: Some of the risk areas are;


