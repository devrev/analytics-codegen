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

### Widget Structure Template

```json
{
  "data_sources": [
    {
      "type": "oasis",
      "reference_name": "your_source_name",
      "dimensions": [
        {
          "reference_name": "your_dimension"
          // ... dimension configuration
        }
      ],
      "measures": [
        {
          "reference_name": "your_measure"
          // ... measure configuration
        }
      ]
    }
  ],
  "sub_widgets": [
    {
      "query": {
        "dimensions": ["your_source_name.your_dimension"],
        "measures": ["your_source_name.your_measure"],
        "order_by": [
          {
            "direction": "ascending",
            "reference_name": "your_source_name.your_dimension"
          }
        ]
      },
      "visualization": {
        "type": "line",
        "line": {
          "x": [
            {
              "label": "Your X-Axis Label",
              "reference_name": "your_source_name.your_dimension"
            }
          ],
          "y": [
            {
              "label": "Your Y-Axis Label",
              "reference_name": "your_source_name.your_measure"
            }
          ]
        }
      }
    }
  ]
}
```

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

#### d. Supported Field Types in DevRev

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
    "field_type": "timestamp", // One of the supported field types
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

5. **SQL SELECT STATEMENT RULES**

Your base query in `sql_query` MUST follow these rules:

a. ✅ MANDATORY: List EVERY column individually with its table name

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

### Critical Rules for Query References and Visualization

#### 1. MANDATORY REFERENCE NAMING

Every dimension and measure MUST be referenced with its data source name:

```json
// 🚫 NEVER DO THIS:
"dimensions": ["dimension_name"]

// ✅ ALWAYS DO THIS:
"dimensions": ["data_source_name.dimension_name"]
```

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

2. **Visualization Structure**

- Table Structure

"visualization": {
"table": {
"columns": [
{
"label": "Account",
"reference_name": "support_insights_ticket_metrics_summary.account_id",
"order": 1
},
{
"label": "Count",
"reference_name": "support_insights_ticket_metrics_summary.unique_ids_count"
}
]
},
"type": "table"
}

- To enable GroupBy in Table add is_groupable in dimension
  { "ui": { "is_groupable": true } }

- Line Chart Structure

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

- Bar/Horizontal bar chart

  - NOTE: is_stacked is optional and it is used when you have done group by twice

    "visualization": {
    "bar": {
    "is_stacked": false,
    "x": [
    {
    "label": "Stage",
    "reference_name": "support_insights_ticket_stage_time_metrics_summary.stage_id"
    }
    ],
    "y": [
    {
    "label": "Average Total Duration",
    "reference_name": "support_insights_ticket_stage_time_metrics_summary.average_total_duration"
    }
    ]
    },
    "type": "bar"
    }

- Column/Vertical bar chart)
  - is_stacked MUST be optional and it is used when you have done group by twice
  - This example is with stacked true and color object indicates which key to what color

"visualization": {
"column": {
"is_stacked": true,
"x": [
{
"label": "Date",
"reference_name": "support_insights_ticket_metrics_summary.record_date"
},
{
"color": {
"key_lookup": [
{
"key": "breached",
"value": "chart-category-6-base"
},
{
"key": "warning",
"value": "chart-category-2-base"
},
{
"key": "paused",
"value": "chart-category-7-base"
}
],
"type": "key_lookup"
},
"label": "Stage",
"reference_name": "support_insights_ticket_metrics_summary.sla_stage"
}
],
"y": [
{
"label": "Count",
"reference_name": "support_insights_ticket_metrics_summary.count_sla_stage"
}
]
},
"type": "column"
}

- PackedBubble

"visualization": {
"packed_bubble": {
"x": [
{
"label": "Date",
"reference_name": "support_insights_ticket_metrics_summary.record_date"
},
{
"color": {
"key_lookup": [
{
"key": "breached",
"value": "chart-category-6-base"
},
{
"key": "warning",
"value": "chart-category-2-base"
},
{
"key": "paused",
"value": "chart-category-7-base"
}
],
"type": "key_lookup"
},
"label": "Stage",
"reference_name": "support_insights_ticket_metrics_summary.sla_stage"
}
],
"y": [
{
"label": "Count",
"reference_name": "support_insights_ticket_metrics_summary.count_sla_stage"
}
]
},
"type": "packed_bubble"
}

- Donut

"visualization": {
"donut": {
"x": [
{
"color": {
"key_lookup": [
{
"key": "1",
"value": "chart-alert-base"
},
{
"key": "2",
"value": "chart-alert-lighter"
},
{
"key": "3",
"value": "chart-neutrals-lighter"
}
],
"type": "key_lookup"
},
"label": "CSAT Score",
"reference_name": "support_insights_conversation_metrics_summary.csat_score"
}
],
"y": {
"label": "Count",
"reference_name": "support_insights_conversation_metrics_summary.count_star"
}
},
"type": "donut"
}

- Pie chart

"visualization": {
"pie": {
"x": [
{
"color": {
"key_lookup": [
{
"key": "1",
"value": "chart-alert-base"
},
{
"key": "2",
"value": "chart-alert-lighter"
},
{
"key": "3",
"value": "chart-neutrals-lighter"
}
],
"type": "key_lookup"
},
"label": "CSAT Score",
"reference_name": "support_insights_conversation_metrics_summary.csat_score"
}
],
"y": {
"label": "Count",
"reference_name": "support_insights_conversation_metrics_summary.count_star"
}
},
"type": "pie"
}

- Heatmap

{
"heatmap": {
"x": {
"label": "Created Date",
"reference_name": "dim_conversation.created_date"
},
"y": {
"label": "Source",
"reference_name": "dim_conversation.owned_by_id"
},
"z": {
"color": {
"static": "chart-category-3-base",
"type": "static"
},
"drill_throughs": [
{
"dashboard": "don:data:dvrv-us-1:devo/0:dashboard/1U5KEFvaCV",
"dashboard_v1": "don:DEV-0:dashboard:1U5KEFvaCV",
"label": "drill"
}
],
"label": "Count",
"reference_name": "dim_conversation.avg_first_response_time"
}
},
"type": "heatmap"
}

- Metric

"visualization": {
"metric": {
"y": [
{
"label": "Average Rating",
"reference_name": "support_insights_ticket_metrics_summary.average_rating"
}
]
},
"type": "metric"
}

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
     "reference_name": "your_source_name" // This name must be used to qualify fields
     // ... other configuration
   }
   ```

2. **Dimension and Measure References**
   - Must include data source reference name
   - Format: `your_source_name.field_name`
   - Example: `your_source_name.your_dimension`

### Common Errors and Solutions

#### SQL Parser Errors with SELECT

⚠️ IF YOU SEE THESE ERRORS:

Error: Parser Error: syntax error at or near ","
LINE 1: SELECT, FROM ...

IT MEANS:

- You used _ or table._ in your SELECT
- You didn't fully qualify your columns
- You need to list each column individually

Error: Parser Error: syntax error at or near ","
LINE 1: SELECT, FROM ...

#### Reference Name Errors

Error: Cannot find reference 'field_name'

Solution:

- Ensure all references include data source name
- Verify the reference_name exists in dimensions/measures
- Check for typos in reference names

#### Other Errors

1. Error: Failed to create widget - unexpected discriminator: string

### Best Practices Checklist

IMPORTANT: MUST follow before submitting a widget configuration:

1. ✓ All dimension/measure references include data source name
2. ✓ Visualization structure matches the documented format
3. ✓ Query includes required order_by for time series
4. ✓ Reference names are consistent throughout the configuration
5. ✓ Data source reference_name matches primary data source

```

```
