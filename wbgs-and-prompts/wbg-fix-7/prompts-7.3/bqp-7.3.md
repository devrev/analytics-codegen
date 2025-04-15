# Base Query Prompt

Validate data types before comparison

```sql
-- Check column types
SELECT column_name, data_type FROM information_schema.columns
WHERE table_name = 'table_name';

-- Use appropriate casts when comparing different types
WHERE CAST(string_date AS DATE) = DATE '2023-01-01'
```

Verify data existence before filtering

```sql
-- Check data boundaries and availability
SELECT MIN(date_column), MAX(date_column), COUNT(*)
FROM table_name;
```

Build queries incrementally

```sql
-- Start simple, then add complexity
SELECT * FROM table LIMIT 5;
-- Then add WHERE, GROUP BY, HAVING, etc.
```

Test aggregate thresholds separately

```sql
-- Validate aggregates before applying HAVING
SELECT service, SUM(cost) FROM table
GROUP BY service ORDER BY SUM(cost) DESC LIMIT 10;
```

Check date formats and functions

```sql
-- Verify date handling works as expected
SELECT DISTINCT date_column,
       CAST(date_column AS DATE),
       DATE_TRUNC('month', CAST(date_column AS DATE))
FROM table LIMIT 5;
Use explicit data types and formats
Specify date formats clearly: DATE '2023-01-01'
Use explicit casts: CAST(column AS TYPE)
Declare function return types when necessary
```

Use explicit data types and formats:
Specify date formats clearly: DATE '2023-01-01'
Use explicit casts: CAST(column AS TYPE)
Declare function return types when necessary

Comment liberally on assumptions

```sql
-- Assuming usage_date is stored as VARCHAR in YYYY-MM-DD format
WHERE CAST(usage_date AS DATE) >= DATE '2023-01-01'
```

Verify data types - Run DESCRIBE table_name before writing complex queries
Use explicit casting - Always cast string dates: CAST(col AS DATE) or col::DATE
Match join column types - Ensure join columns have compatible formats
Handle NULL values - Use NULLIF(divisor, 0) for divisions
Test components first - Validate critical operations with sample data

```sql
-- Quick pre-check
DESCRIBE my_table;

-- Test critical components
SELECT
    col_name,
    CAST(date_col AS DATE) AS formatted_date
FROM my_table
LIMIT 3;
```

Use relative dates (CURRENT_DATE - INTERVAL)
Prevent division errors with NULLIF()
Handle boolean values with explicit CASE WHEN
Cast numeric types appropriately (::FLOAT)
Start with lower thresholds, scale up if needed

```sql
SELECT
    [dimensions],
    COUNT(*) AS count,
    COUNT(DISTINCT id) AS unique_count,
    SUM(CASE WHEN condition THEN 1 ELSE 0 END) AS event_count,
    SUM(value)::FLOAT / NULLIF(COUNT(*), 0) AS avg_value
FROM table
WHERE date_col >= CURRENT_DATE - INTERVAL '30 days'
GROUP BY [dimensions]
HAVING COUNT(*) >= 10
ORDER BY count DESC;
```
