# Query Generation

Understand how the widget system works, after the JSON is compiled.
It automatically generates SQL queries based on your configuration.
For example:

It starts with your base query from `oasis.sql_query`
Applies filters based on dimensions
Adds aggregations from measures
Applies sorting and grouping

## Best Practices

Use full table names in the base query when possible
If using aliases, keep them simple and descriptive
Document table relationships in comments
Always test the base query independently first
If it has errors, fix those before proceeding.
Remember that the widget system generates additional SQL on top of your base query
The generated SQL wraps your base query in a subquery
Aliases from your base query may not be available in outer queries

## Understanding the Query Generation Process

The widget system transforms your base query through several layers:

Base Layer, the original SQL base query:

```sql
SELECT article_views_and_votes_summary., dim_article.title
FROM system.article_views_and_votes_summary
LEFT OUTER JOIN system.dim_article
ON article_views_and_votes_summary.article_id = dim_article.id
```

Measure Layer, system-generated:

```sql
SELECT
SUM(total_views) as article_views_summarytotal_views,
SUM(unique_views) as article_views_summaryunique_views
FROM (
-- Your base query is inserted here
SELECT article_views_and_votes_summary., dim_article.title
FROM system.article_views_and_votes_summary
LEFT OUTER JOIN system.dim_article
ON article_views_and_votes_summary.article_id = dim_article.id
) AS article_views_summary
```

Filter Layer, system-generated):

```sql
SELECT FROM (
-- Measure layer query is inserted here
) AS filtered_query
WHERE record_date >= '2024-01-01'
GROUP BY article_id
```

Key Points to Remember:

Table aliases from your base query are not accessible in measure definitions
The system automatically adds its own aliases to the generated query
Column references in measures and dimensions should use the raw column name
When in doubt, use full table names in the base query instead of aliases

Common Pitfalls to watch out for:

DO NOT:
Use table aliases in measure SQL expressions
Reference base query aliases in dimension definitions
Complicate subqueries with conflicting aliases

### Important Rules for Base Queries and Column References

Table Aliases in Generated Queries:

Table aliases from your base query are NOT preserved in the generated outer queries
Do NOT use table aliases in `sql_expression` fields
Make column selections explicit in your base query

Correct vs Incorrect Examples:

Incorrect Approach:

```json
{
  "sql_query": "SELECT FROM table1 t1 JOIN table2 t2 ON t1.id = t2.id",
  "dimensions": [
    {
      "meerkat_schema": {
        "sql_expression": "t2.column_name", // WRONG: using table alias
        "type": "string"
      }
    }
  ]
}
```

Correct Approach:

```json
{
  "sql_query": "SELECT t1., t2.column_name FROM table1 t1 JOIN table2 t2 ON t1.id = t2.id",
  "dimensions": [
    {
      "meerkat_schema": {
        "sql_expression": "column_name", // RIGHT: using just the column name
        "type": "string"
      }
    }
  ]
}
```

Best Practices:

Make column selections explicit in your base query
Avoid using \* in SELECT statements when possible
Don't rely on table aliases in sql_expression fields
Use clear, unique column names to avoid ambiguity

#### SQL SELECT Statement Rules

Your base query in `sql_query` MUST follow these rules:

MANDATORY: List EVERY column individually with its table name

```sql
-- CORRECT AND REQUIRED FORMAT:
SELECT
    table1.column1,
    table1.column2,
    table2.column3
FROM schema.table1
JOIN schema.table2 ON table1.id = table2.id

-- INCORRECT: DO NOT PERFORM ANY OF THESE:
SELECT *                                    -- BREAKS
SELECT table.*                             -- BREAKS
SELECT column1, column2                    -- BREAKS
SELECT table1.*, table2.column3           -- BREAKS
```
