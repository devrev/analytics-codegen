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

According to the widget-building guide, base query and table schemas, generate a JSON file for the widget.
