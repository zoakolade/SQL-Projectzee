What issues will you address by cleaning the data?
The nulls, the irregular datatype and missing values in the data





Queries: 
```sql
SELECT *
FROM sales_report
WHERE productsku IS NULL;

SELECT *
FROM sales_report
WHERE total_ordered IS NULL;

SELECT *
FROM sales_report
WHERE name IS NULL;

SELECT *
FROM sales_report
WHERE stockLevel IS NULL;

SELECT *
FROM sales_report
WHERE restockingLeadTime IS NULL;

SELECT *
FROM sales_report
WHERE sentimentScore IS NULL;

SELECT *
FROM sales_report
WHERE sentimentMagnitude IS NULL;

SELECT *
FROM sales_report
WHERE ratio IS NULL;
```


Below, provide the SQL queries you used to clean your data.
```sql
UPDATE all_sessions
SET city =
CASE
WHEN city ='(not set)' THEN country
WHEN city is null THEN country
WHEN city = 'not available in demo dataset' THEN country
WHEN city IN ('(not set)', 'not available in demo dataset')
THEN (CASE WHEN country NOT IN('(not set)')
THEN country
END)
ELSE COALESCE (city, country)
END;

ALTER TABLE all_sessions
ADD new_time_column TIME;

UPDATE all_sessions
SET new_time_column = make_interval(secs => time);

ALTER TABLE all_sessions
ADD new_date_column DATE;

UPDATE all_sessions
SET new_date_column = DATE 'epoch' + date * INTERVAL '1 second';

ALTER TABLE all_sessions
DROP COLUMN date;

select timeonsite, new_date_column, new_time_column
from all_sessions;
```
