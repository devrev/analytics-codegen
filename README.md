# Analytics Code Generation

## Objective

Use GenAI to generate JSON file for widget

Input:

- MD file with rules for widget generation
- Schema of all tables
- Base query that fines final data table for widget

Output:

- JSON file that generates widget
- Manually-inserted into JSON editor for results

## Specifics

### Model: Claude 3.7 SOnnet

Using Trae AI

- Equipped with same model as Cursor Pro

#### Prompt

<Insert 'wbg-\*.md' file>

Base query:

<Insert SQL query for tables here>

Schema:

<Insert schema of each table in base query here>

<Should be separated by a new line, if multiple entries>

Understand the files attached fully for how to build a widget, including data sources. Provide a JSON file to generate a visualization, according to the base query, table schemas and attached guide above.
