# Base Query Prompt

Rules to create base query:
SELECT only necessary columns, according to what the widget should display.
Do not use any table aliases. Use entire table names, instead.
Do not use any aggregate functions, only the column names themselves.
Add NULL-value handling to take care of any non-existent data in query.
Ensure the WHERE clause handles negative and empty values.
Only use ORDER BY or GROUP BY when necessary.
Do not add extra columns or clauses, i.e. COALESCE, to query.
Do not add any comments to the query.
