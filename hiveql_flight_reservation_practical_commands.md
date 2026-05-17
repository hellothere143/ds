# Flight Reservation HiveQL Practical Commands

## Step 1: Create Database
Purpose: Create a new database for the practical.

```sql
CREATE DATABASE flightdb;
```

---

## Step 2: Use Database
Purpose: Select the database to work on.

```sql
USE flightdb;
```

---

## Step 3: Create Flights Table
Purpose: Create table for storing flight dataset.

```sql
CREATE TABLE flights (
    Year INT,
    Month INT,
    DayofMonth INT,
    DepTime INT,
    ArrTime INT,
    UniqueCarrier STRING,
    FlightNum INT,
    ArrDelay INT,
    DepDelay INT,
    Origin STRING,
    Dest STRING,
    Distance INT
)
ROW FORMAT DELIMITED
FIELDS TERMINATED BY ','
STORED AS TEXTFILE
TBLPROPERTIES ("skip.header.line.count"="1");
```

---

## Step 4: Load Dataset into Table
Purpose: Load 2007.csv dataset into flights table.

```sql
LOAD DATA LOCAL INPATH '/home/hadoop/2007.csv'
INTO TABLE flights;
```

Note: Change file path according to your system.

---

## Step 5: Display All Data
Purpose: Show complete table data.

```sql
SELECT * FROM flights;
```

---

## Step 6: Display Limited Records
Purpose: Show only first 10 rows.

```sql
SELECT * FROM flights LIMIT 10;
```

---

## Step 7: Count Total Records
Purpose: Count total rows in table.

```sql
SELECT COUNT(*) FROM flights;
```

---

## Step 8: Describe Table
Purpose: Show table structure.

```sql
DESCRIBE flights;
```

---

## Step 9: Alter Table
Purpose: Add new column in table.

```sql
ALTER TABLE flights
ADD COLUMNS (Status STRING);
```

---

## Step 10: Create Index
Purpose: Create index on Origin column.

```sql
CREATE INDEX flight_index
ON TABLE flights (Origin)
AS 'COMPACT'
WITH DEFERRED REBUILD;
```

---

## Step 11: Rebuild Index
Purpose: Activate and rebuild index.

```sql
ALTER INDEX flight_index
ON flights REBUILD;
```

---

## Step 12: Create Airport Table
Purpose: Create second table for JOIN operation.

```sql
CREATE TABLE airport (
    code STRING,
    city STRING
)
ROW FORMAT DELIMITED
FIELDS TERMINATED BY ','
STORED AS TEXTFILE;
```

---

## Step 13: Insert Data into Airport Table
Purpose: Insert sample airport data.

```sql
INSERT INTO airport VALUES
('SAN','San Diego'),
('SFO','San Francisco'),
('LAX','Los Angeles');
```

---

## Step 14: Perform JOIN Operation
Purpose: Join flights and airport tables.

```sql
SELECT f.Origin, a.city, f.Dest
FROM flights f
JOIN airport a
ON (f.Origin = a.code);
```

---

## Step 15: Drop Flights Table
Purpose: Delete table after practical completion.

```sql
DROP TABLE flights;
```

---

# Final Execution Order

1. CREATE DATABASE
2. USE DATABASE
3. CREATE TABLE
4. LOAD DATA
5. DISPLAY DATA
6. LIMIT QUERY
7. COUNT QUERY
8. DESCRIBE TABLE
9. ALTER TABLE
10. CREATE INDEX
11. REBUILD INDEX
12. CREATE SECOND TABLE
13. INSERT VALUES
14. JOIN QUERY
15. DROP TABLE

