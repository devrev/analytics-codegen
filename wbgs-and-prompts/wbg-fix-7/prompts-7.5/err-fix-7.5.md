# Ex 2 Incident Count IP vs. Closed

1. Don't pre-transform data in SQL queries
   Instead, use raw columns in queries and define transformations in dimensions:

```json
// SQL query - keep simple with raw columns
"sql_query": "SELECT created_date, state, id FROM system.dim_incident WHERE is_deleted = FALSE"

// Define transformations in dimensions
"dimensions": [
  {
    "meerkat_schema": {
      "sql_expression": "date_trunc('month', created_date)",
      "type": "time"
    },
    "reference_name": "created_month"
  }
]
```

2. Don't pre-aggregate data in SQL when using measures
   Instead, pull raw data and define aggregations in measures:

```json
// SQL query - raw data only
"sql_query": "SELECT created_date, state, id FROM system.dim_incident"

// Define aggregations in measures
"measures": [
  {
    "meerkat_schema": {
      "sql_expression": "COUNT(id)",
      "type": "number"
    },
    "reference_name": "incident_count"
  }
]
```

3. Don't use empty or incomplete SELECT clauses
   Always include explicit column selections:

```json
// Always select specific columns
"sql_query": "SELECT created_date, state, id FROM system.dim_incident WHERE is_deleted = FALSE"
```

4. Don't mix reference naming patterns
   Use consistent, fully-qualified reference names:

```json
// Data source
"reference_name": "dim_incident"

// Sub-widget query
"dimensions": ["dim_incident.created_month", "dim_incident.incident_status"]

// Visualization
"reference_name": "dim_incident.incident_count"
```

5. Don't reference columns that don't exist in the data source
   Only reference columns that are available from your SQL query:

```json
// SQL query defines available columns
"sql_query": "SELECT created_date, state, id FROM system.dim_incident"

// Only reference these columns in dimensions/measures
"sql_expression": "CASE WHEN state IN ('CLOSED', 'RESOLVED') THEN 'Closed' ELSE 'In Progress' END"
```

# #x 4 Reader Engagement Score

3. Group By Visualization with Categories

```json
"query": {
  "dimensions": [
    "my_data_source.created_date",
    "my_data_source.category"
  ],
  "measures": [
    "my_data_source.count"
  ],
  "order_by": [
    {
      "direction": "ascending",
      "reference_name": "my_data_source.created_date"
    }
  ]
}
```

4. Boolean Field Handling

```json
"dimensions": [
  {
    "devrev_schema": {
      "field_type": "text",
      "is_filterable": true,
      "name": "status_type",
      "ui": {
        "display_name": "Status"
      }
    },
    "meerkat_schema": {
      "sql_expression": "CASE WHEN is_active THEN 'Active' ELSE 'Inactive' END",
      "type": "string"
    },
    "reference_name": "status_type"
  }
]
```

5. Safe Numeric Calculations

```json
"measures": [
  {
    "devrev_schema": {
      "field_type": "double",
      "is_filterable": false,
      "name": "average_value",
      "ui": {
        "display_name": "Average Value"
      }
    },
    "meerkat_schema": {
      "sql_expression": "SUM(value) / NULLIF(COUNT(*), 0)",
      "type": "number"
    },
    "reference_name": "average_value"
  }
]
```

6. Percentage Formatting

```json
"measures": [
  {
    "devrev_schema": {
      "field_type": "double",
      "name": "completion_rate",
      "ui": {
        "display_name": "Completion Rate",
        "unit": "percentage"
      }
    },
    "meerkat_schema": {
      "sql_expression": "100.0 * COUNT(CASE WHEN status = 'completed' THEN 1 END) / NULLIF(COUNT(*), 0)",
      "type": "number"
    },
    "reference_name": "completion_rate"
  }
]
```

7. Simple Table Visualization

```json
"visualization": {
  "table": {
    "columns": [
      {
        "label": "Date",
        "reference_name": "my_data_source.created_date"
      },
      {
        "label": "Category",
        "reference_name": "my_data_source.category"
      },
      {
        "label": "Count",
        "reference_name": "my_data_source.count"
      }
    ]
  },
  "type": "table"
}
```
