What are your risk areas? Identify and describe them.



QA Process: Some of the risk areas are;

I. Data Loss: Deleting or altering data without proper backups can result in irreversible damage therefore while importing the data I did not delete or alter any of the details provided. I created the tables then imported the csv.files without altering any detail
II. Data Integrity: Enforcing data integrity constraints like primary keys and foreign keys help maintain data quality. Therefore PK and FK was defined for the dimension and fact table.
III. Data Type Conversion: Incorrectly converting data types can lead to loss of precision or unexpected results therefore I needed to look into the data and determine what the correct data type should be and write the appropriate query for conversion.
IV. Null Values: The data contains a lot of Null values which if not properly handled can skew analysis and lead to incorrect conclusions. In the sale_report table where column is ratio there lots of NULL when cleaned
V. Join Operations: Using inappropriate join conditions can lead to incorrect or incomplete results. Therefore I used subqueries where possible to double my results.
Describe your QA process and include the SQL queries used to execute it.
