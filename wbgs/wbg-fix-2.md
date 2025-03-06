# 🛑 STOP - READ THIS FIRST - SQL RULES 🛑

### SQL SELECT STATEMENT RULES
Your base query in `sql_query` MUST follow these rules:

1. ✅ MANDATORY: List EVERY column individually with its table name
```sql
-- ✅ CORRECT AND REQUIRED FORMAT:
SELECT 
    table1.column1,
    table1.column2,
    table2.column3
FROM schema.table1
JOIN schema.table2 ON table1.id = table2.id

-- 🚫 ANY OF THESE WILL BREAK YOUR WIDGET:
SELECT *                                    -- BREAKS
SELECT table.*                             -- BREAKS
SELECT column1, column2                    -- BREAKS
SELECT table1.*, table2.column3           -- BREAKS
```
3. ⚠️ IF YOU SEE THIS ERROR:

Error: Parser Error: syntax error at or near ","
LINE 1: SELECT, FROM ...

IT MEANS:
1. You used * or table.* in your SELECT
2. You didn't fully qualify your columns
3. You need to list each column individually

# ⚠️ REQUIRED RULES - READ FIRST ⚠️

### 1. MANDATORY REFERENCE NAMING
Every dimension and measure MUST be referenced with its data source name:
```json
// 🚫 NEVER DO THIS:
"dimensions": ["dimension_name"]

// ✅ ALWAYS DO THIS:
"dimensions": ["data_source_name.dimension_name"]
```

### 2. MANDATORY LINE CHART STRUCTURE
Line charts MUST follow this exact structure:
```json
"visualization": {
  "type": "line",
  "line": {  // 🚫 NEVER use "settings"
    "x": [{
      "label": "Label",
      "reference_name": "data_source_name.dimension_name"  // MUST include data source name
    }],
    "y": [{
      "label": "Label",
      "reference_name": "data_source_name.measure_name"    // MUST include data source name
    }]
  }
}
```

### 3. MANDATORY QUERY STRUCTURE
Queries MUST follow this exact structure:
```json
"query": {
  "dimensions": ["data_source_name.dimension_name"],     // MUST include data source name
  "measures": ["data_source_name.measure_name"],        // MUST include data source name
  "order_by": [{                                        // Required for time series
    "direction": "ascending",
    "reference_name": "data_source_name.dimension_name" // MUST include data source name
  }]
}
```

### 4. COMMON ERRORS TO AVOID
1. 🚫 NEVER use unqualified names (without data source prefix)
2. 🚫 NEVER use "settings" in line chart visualization
3. 🚫 NEVER skip the order_by for time series
4. 🚫 NEVER use table aliases in sql_expression fields

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
   - Avoid using * in SELECT statements when possible
   - Don't rely on table aliases in sql_expression fields
   - Use clear, unique column names to avoid ambiguity

### Supported Field Types in DevRev

When defining dimensions and measures, DevRev supports the following field types:

1. **Numeric Types**
   - `int`: Integer values
   - `double`: Floating-point numbers
   - `decimal`: Precise decimal numbers
   - `currency`: Monetary values

2. **Boolean Type**
   - `bool`: True/false values

3. **Text Types**
   - `string`: Basic string values
   - `text`: Longer text content
   - `tokens`: Tokenized text for search/filtering
   - `rich_text`: Formatted text with markup
   - `bytes`: Binary data

4. **Time Type**
   - `timestamp`: Date and time values

5. **Reference Types**
   - `id`: Unique identifiers
   - `overridable_enum`: Enumerated values that can be overridden
   - `uenum`: User-defined enumeration
   - `reference_enum`: Reference to enumerated values

Example usage in dimension definition:

```json
{
    "devrev_schema": {
        "field_type": "timestamp",  // One of the supported field types
        "db_name": "created_date",
        "is_filterable": true,
        "name": "created_date",
        "ui": {
            "display_name": "Creation Date"
        }
    },
    "meerkat_schema": {
        "sql_expression": "created_date",
        "type": "time"
    }
}
```

When choosing field types:
- Use appropriate numeric types (`int`, `double`, `decimal`) based on precision needs
- Choose between text types based on content and search requirements
- Use `timestamp` for all date/time fields to ensure proper filtering
- Select correct enumeration type (`overridable_enum`, `uenum`, `reference_enum`) based on value source

### Critical Rules for Query References and Visualization

1. **Dimension and Measure References in Queries**
   ```json
   // ❌ INCORRECT - unqualified references
   "query": {
     "dimensions": ["some_dimension"],
     "measures": ["some_measure"]
   }
   
   // ✅ CORRECT - fully qualified with data source
   "query": {
     "dimensions": ["your_source_name.some_dimension"],
     "measures": ["your_source_name.some_measure"]
   }
   ```

2. **Line Chart Visualization Structure**
   ```json
   // ❌ INCORRECT structure
   "visualization": {
     "type": "line",
     "settings": {
       "x_axis": "dimension_name",
       "y_axis": "measure_name"
     }
   }
   
   // ✅ CORRECT structure
   "visualization": {
     "type": "line",
     "line": {
       "x": [{
         "label": "Your X-Axis Label",
         "reference_name": "your_source_name.dimension_name"
       }],
       "y": [{
         "label": "Your Y-Axis Label",
         "reference_name": "your_source_name.measure_name"
       }]
     }
   }
   ```

3. **Required Query Components**
   ```json
   "query": {
     "dimensions": ["your_source_name.your_dimension"],
     "measures": ["your_source_name.your_measure"],
     "order_by": [{                    // Required for time series
       "direction": "ascending",
       "reference_name": "your_source_name.your_dimension"
     }]
   }
   ```

### Reference Name Rules

1. **Data Source Reference Names**
   - Must be unique within the widget
   - Should match the primary table/view name
   - Used to qualify all dimension and measure references
   ```json
   {
     "type": "oasis",
     "reference_name": "your_source_name",  // This name must be used to qualify fields
     // ... other configuration
   }
   ```

2. **Dimension and Measure References**
   - Must include data source reference name
   - Format: `your_source_name.field_name`
   - Example: `your_source_name.your_dimension`

### Common Errors and Solutions

1. **SQL Parser Error with SELECT**
   ```
   Error: Parser Error: syntax error at or near "," 
   LINE 1: SELECT, FROM ...
   ```
   This typically occurs when:
   - Dimension/measure references are not fully qualified
   - Query structure is missing required components
   
   Solution:
   - Always use fully qualified names
   - Include all required query components
   - Follow the correct visualization structure

2. **Reference Not Found Errors**
   ```
   Error: Cannot find reference 'field_name'
   ```
   Solution:
   - Ensure all references include data source name
   - Verify the reference_name exists in dimensions/measures
   - Check for typos in reference names

### Widget Structure Template
```json
{
  "data_sources": [{
    "type": "oasis",
    "reference_name": "your_source_name",
    "dimensions": [{
      "reference_name": "your_dimension",
      // ... dimension configuration
    }],
    "measures": [{
      "reference_name": "your_measure",
      // ... measure configuration
    }]
  }],
  "sub_widgets": [{
    "query": {
      "dimensions": ["your_source_name.your_dimension"],
      "measures": ["your_source_name.your_measure"],
      "order_by": [{
        "direction": "ascending",
        "reference_name": "your_source_name.your_dimension"
      }]
    },
    "visualization": {
      "type": "line",
      "line": {
        "x": [{
          "label": "Your X-Axis Label",
          "reference_name": "your_source_name.your_dimension"
        }],
        "y": [{
          "label": "Your Y-Axis Label",
          "reference_name": "your_source_name.your_measure"
        }]
      }
    }
  }]
}
```

### Best Practices Checklist

Before submitting a widget configuration:
1. ✓ All dimension/measure references include data source name
2. ✓ Visualization structure matches the documented format
3. ✓ Query includes required order_by for time series
4. ✓ Reference names are consistent throughout the configuration
5. ✓ Data source reference_name matches primary data source

