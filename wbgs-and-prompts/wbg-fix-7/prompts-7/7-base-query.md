# Base Query

Change base query before inserting in sample widget template below.
Remove all table aliases and use entire table names in query.
Replace aggregate functions with only the column names in query.
Filter only necessary columns for widget generation in query.
Add NULL-value handling to take care of any non-existent data in query.
Ensure WHERE clause handles negative and empty values.

## Extra, if needed:

Also, try the following, if applicable:

For metrics and measures:
Apply appropriate aggregation functions (SUM, AVG, COUNT) to all measure columns.
Always use COALESCE(column, 0) inside aggregation functions to handle NULL values.

For dimensions (non-aggregated columns):
Include ALL dimension columns in the GROUP BY clause.
For time-series visualizations, always include date/timestamp columns in GROUP BY clause.

For mixed columns (sometimes grouped, sometimes aggregated):
When a column appears in both dimension and measure contexts, use aggregation in the measure.
Example:

```sql
SUM(COALESCE(unique_views, 0)) as total_unique_views
```

for measures.
Use the raw column in GROUP BY for dimensions.

For columns where exact values aren't important but needed for display:
Use ANY_VALUE() function.
Example:

```sql
ANY_VALUE(title) AS title
```

Don't include these in GROUP BY unless needed for accurate grouping.

Always test queries with explicit GROUP BY clauses before finalizing widgets.

For time-series data, consider adding date truncation functions

```sql
DATE_TRUNC('day', timestamp_col)
```
