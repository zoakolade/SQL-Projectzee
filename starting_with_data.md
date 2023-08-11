Question 1: What will you do to normalize your data?

SQL Queries:
```sql
CREATE TABLE Orders (
OrderID INT PRIMARY KEY,
CustomerID INT,
ProductID INT,
Quantity INT,
OrderDate DATE,
FOREIGN KEY (CustomerID) REFERENCES Customers(CustomerID),
FOREIGN KEY (ProductID) REFERENCES Products(ProductID)
);
```

Answer: Table created



Question 2: In what year did the first visit occur and time?

SQL Queries:
```sql
select visitid, new_date_column, new_time_column
from all_sessions
Order by timeonsite desc nulls last;
```

Answer: Date = 1970-08-22 and time was 07:22:16



Question 3: How will I fix structural errors in the data

SQL Queries: 
```sql
SELECT city, country, v2productcategory,date
IF (state IN ( '(not set)', 'not available in demo dataset', NULL) state
FROM all_sessions;
```

Answer: inappropriate values replaced



Question 4: Change the data type for date and time

SQL Queries:
```sql
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
ALTER TABLE all_sessions
DROP COLUMN time;
```

Answer: New data type for time and date updated



Question 5: Which visitid has the highest time on site

SQL Queries:
```sql
select visitid, max(timeonsite)as timeonsite , new_date_column, new_time_column
from all_sessions
Group by visitid, timeonsite, new_date_column, new_time_column
Order by timeonsite desc nulls last;
```

Answer: 1479144257
