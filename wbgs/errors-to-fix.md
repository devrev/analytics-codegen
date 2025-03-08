# Errors and Fixes

#### SQL Parser Errors with SELECT

Error: Parser Error: syntax error at or near ","
LINE 1: SELECT, FROM ...

Fix:

- You used _ or table._ in your SELECT
- You didn't fully qualify your columns
- You need to list each column individually

Error: Parser Error: syntax error at or near ","
LINE 1: SELECT, FROM ...

#### Reference Name Errors

Error: Cannot find reference 'field_name'

Fix:

- Ensure all references include data source name
- Verify the reference_name exists in dimensions/measures
- Check for typos in reference names

## Field Types Errors

Error: Failed to create widget - Missing required field: reference_name

## Visualization Errors

Error: Failed to create widget - unexpected discriminator: string
