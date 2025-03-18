# Add to Prompt

## Suggestions

1. Reasoning behind error fixes
2. Reference name vs. ID difference
3. Field types
   - Add all enum values from docs
   - Add all DevRev schema `allowed_values` for certain fields
   - Look at cheat-sheet for more info
4. How each part relates to another
   - Base qeury, give examples
     - Change examples to general case, w/o explicit table names
     - Give different examples of query types, i.e. single table, two tables, joins
   - For data source:
     - Explain DevRev vs. meerkat schema
     - Explain how model should interpret schema from user-provided table schema
     - Either choose to call the datasets "tables" or "datasets" - consistency
   - Within sub-widgets, each sub-widget has its own query and visualization section
     - Query has corresponding dimensions / measures and (?) SQL order by clause (?)
     - Visualization for each query, wiht reference names/IDs matching

## Fixes

1. Code-snippet formatting/errors
   - Brackets for data source section: [], but model giving {}
2. Ask model what to add as instructions
