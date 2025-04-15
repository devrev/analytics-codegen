# Widget Building Guide

This guide explains how to create widgets using the JSON editor. The configuration defines data sources, visualizations, and how data should be processed and displayed.

## Widget Configuration Structure

A widget configuration consists of several key sections:

- Data Sources
- Layout
- Sub Widgets
- Visualization Settings

A widget configuration MUST follow this top-level structure:

{
"data_sources": [ // MUST be an array
{
"type": "oasis", // Required
"reference_name": "your_source_name", // Required
// ... other data source properties
}
],
"sub_widgets": [],
"title": "Widget Title"
}

### 1. Data Sources

Each object in the `data_sources` array requires:

- `type`: The source type (usually "oasis")
- `reference_name`: Unique identifier used to reference this source
- `oasis`: Configuration for oasis data
- `dimensions`: Array of dimension definitions
- `measures`: Array of measure definitions

The `data_sources` section is the foundation of your widget. It defines:

#### a. Datasets and Base Query

In the `oasis` section:

"oasis": {
"datasets": [
// List of tables/datasets to use
"system.dataset1",
"system.dataset2"
],
"sql_query": "Your base SQL query here"
}

- `datasets`: List all tables/views that your query will use
- `sql_query`: The base SQL query that joins and processes your data

#### b. Dimensions

Dimensions act as filters on your base query. Each dimension defines:

- `field_type`: The type of field (id, timestamp, enum, bool, tokens, array)
- `db_name`: Database column name
- `name`: Reference name for the field
- `is_filterable`: Whether this field can be used as a filter
- `ui`: Display settings for the field

Example dimension:

{
"devrev_schema": {
"field_type": "timestamp",
"db_name": "record_date",
"is_filterable": true,
"name": "record_date",
"ui": {
"display_name": "Date"
}
},
"meerkat_schema": {
"sql_expression": "record_date",
"type": "time"
}
}

#### c. Measures

Measures define aggregations on your base query. Each measure specifies:

- `field_type`: Data type (int, double, etc.)
- `db_name`: Column name for the measure
- `name`: Reference name
- `ui`: Display settings
- `sql_expression`: The aggregation function to apply

Example measure:

{
"devrev_schema": {
"field_type": "int",
"db_name": "total_views",
"name": "total_views",
"ui": {
"display_name": "Total Views"
}
},
"meerkat_schema": {
"sql_expression": "COUNT(e_article_id)",
"type": "number"
}
}

### 2. Sub Widgets

Sub widgets define how to query and display your data:

"sub_widgets": [{
"query": {
"dimensions": ["dimension1", "dimension2"],
"measures": ["measure1", "measure2"],
"order_by": [{
"direction": "descending",
"reference_name": "measure1"
}]
},
"visualization": {
"type": "table",
"table": {
"columns": [
// Column configurations
]
}
}
}]

### 3. Visualization Types

Common visualization types include:

- `table`: Tabular data display
- `bar`: Bar charts
- `line`: Line graphs
- `pie`: Pie charts

## Query Generation

The system automatically generates SQL queries based on your configuration. It:

1. Starts with your base query from `oasis.sql_query`
2. Applies filters based on dimensions
3. Adds aggregations from measures
4. Applies sorting and grouping

## Best Practices

1. Always test your base query independently first
2. Use meaningful names for dimensions and measures
3. Include appropriate filters in dimensions
4. Consider performance implications of complex joins
5. Use appropriate field types for better UI interaction

## Example Use Case

To create a new widget:

1. Identify required datasets
2. Write and test base query
3. Define dimensions for filtering
4. Define measures for aggregations
5. Configure visualization
6. Test the complete widget

### Best Practices for Table References

1. **Base Query Clarity**

   - Use full table names in the base query when possible
   - If using aliases, keep them simple and descriptive
   - Document table relationships in comments

2. **Column References**

   - In measures and dimensions, use direct column names
   - Avoid table aliases in sql_expression fields
   - Use proper column qualification when names are ambiguous

3. **Query Generation**
   - Remember that the widget system generates additional SQL on top of your base query
   - The generated SQL wraps your base query in a subquery
   - Aliases from your base query may not be available in outer queries

### Understanding Query Generation

The widget system transforms your base query through several layers:

1. **Base Layer** (Your SQL):

SELECT article_views_and_votes_summary., dim_article.title
FROM system.article_views_and_votes_summary
LEFT OUTER JOIN system.dim_article
ON article_views_and_votes_summary.article_id = dim_article.id

2. **Measure Layer** (System Generated):

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

3. **Filter Layer** (System Generated):

SELECT FROM (
-- Measure layer query is inserted here
) AS filtered_query
WHERE record_date >= '2024-01-01'
GROUP BY article_id

**Key Points to Remember:**

1. Table aliases from your base query are not accessible in measure definitions
2. The system automatically adds its own aliases to the generated query
3. Column references in measures and dimensions should use the raw column name
4. When in doubt, use full table names in the base query instead of aliases

**Common Pitfalls:**

- Using table aliases in measure SQL expressions
- Referencing base query aliases in dimension definitions
- Complex subqueries with conflicting aliases

### SQL Query and Column References

#### Important Rules for Base Queries and Column References

1. **Table Aliases in Generated Queries**

   - Table aliases from your base query are NOT preserved in the generated outer queries
   - Do NOT use table aliases in `sql_expression` fields
   - Make column selections explicit in your base query

2. **Correct vs Incorrect Examples**

❌ **Incorrect Approach**:

{
"sql_query": "SELECT FROM table1 t1 JOIN table2 t2 ON t1.id = t2.id",
"dimensions": [{
"meerkat_schema": {
"sql_expression": "t2.column_name", // WRONG: using table alias
"type": "string"
}
}]
}

✅ **Correct Approach**:

{
"sql_query": "SELECT t1., t2.column_name FROM table1 t1 JOIN table2 t2 ON t1.id = t2.id",
"dimensions": [{
"meerkat_schema": {
"sql_expression": "column_name", // RIGHT: using just the column name
"type": "string"
}
}]
}

3. **Common Errors**

   - `Referenced table "X" not found!`: This usually means you're using a table alias in sql_expression
   - Solution: Remove table aliases from sql_expression and make sure columns are explicitly selected in base query

4. **Best Practices**
   - Make column selections explicit in your base query
   - Avoid using \* in SELECT statements when possible
   - Don't rely on table aliases in sql_expression fields
   - Use clear, unique column names to avoid ambiguity
