# Data Sources

## Structure

The `data_sources` array is the first section of the JSON file. It looks something like this:

```json
"data_sources": [
    {
      "dimensions": [
        {
          "devrev_schema": {
            "field_type": "id",
            "id_type": [
              "work"
            ],
            "is_filterable": true,
            "name": "id",
            "ui": {
              "display_name": "Id"
            }
          },
          "meerkat_schema": {
            "sql_expression": "id",
            "type": "string"
          },
          "reference_name": "id"
        },
        {
          "devrev_schema": {
            "allowed_values": [
              "High",
              "Medium",
              "Low",
              "Blocker"
            ],
            "field_type": "enum",
            "is_filterable": true,
            "name": "severity_name",
            "ui": {
              "display_name": "Severity"
            }
          },
          "meerkat_schema": {
            "sql_expression": "severity_name",
            "type": "string"
          },
          "reference_name": "severity_name"
        },
        {
          "devrev_schema": {
            "composite_type": "stage",
            "field_type": "composite",
            "is_filterable": true,
            "name": "stage_id",
            "ui": {
              "display_name": "Stage"
            }
          },
          "meerkat_schema": {
            "sql_expression": "stage_id",
            "type": "string"
          },
          "reference_name": "stage_id"
        },
        {
          "devrev_schema": {
            "field_type": "id",
            "id_type": [
              "account"
            ],
            "is_filterable": true,
            "name": "account_id",
            "ui": {
              "display_name": "Customer"
            }
          },
          "meerkat_schema": {
            "sql_expression": "account_id",
            "type": "string"
          },
          "reference_name": "account_id"
        },
        {
          "devrev_schema": {
            "field_type": "id",
            "id_type": [
              "rev_org"
            ],
            "is_filterable": false,
            "name": "rev_oid",
            "ui": {
              "display_name": "Customer"
            }
          },
          "meerkat_schema": {
            "sql_expression": "rev_oid",
            "type": "string"
          },
          "reference_name": "rev_oid"
        },
        {
          "devrev_schema": {
            "field_type": "timestamp",
            "is_filterable": true,
            "name": "created_date",
            "ui": {
              "display_name": "Created Date"
            }
          },
          "meerkat_schema": {
            "sql_expression": "created_date",
            "type": "time"
          },
          "reference_name": "created_date"
        },
        {
          "devrev_schema": {
            "field_type": "id",
            "id_type": [
              "account"
            ],
            "is_filterable": true,
            "name": "account_id",
            "ui": {
              "display_name": "Account"
            }
          },
          "meerkat_schema": {
            "sql_expression": "account_id",
            "type": "string"
          },
          "reference_name": "account_id"
        },
        {
          "devrev_schema": {
            "field_type": "id",
            "id_type": [
              "part"
            ],
            "is_filterable": true,
            "name": "primary_part_id",
            "ui": {
              "display_name": "Part"
            }
          },
          "meerkat_schema": {
            "sql_expression": "primary_part_id",
            "type": "string"
          },
          "reference_name": "primary_part_id"
        },
        {
          "devrev_schema": {
            "field_type": "id",
            "id_type": [
              "tag"
            ],
            "is_filterable": true,
            "name": "tag_ids",
            "ui": {
              "display_name": "Tag"
            }
          },
          "meerkat_schema": {
            "sql_expression": "tag_ids",
            "type": "string_array"
          },
          "reference_name": "tag_ids"
        },
        {
          "devrev_schema": {
            "field_type": "id",
            "id_type": [
              "group"
            ],
            "is_filterable": true,
            "name": "group_id",
            "ui": {
              "display_name": "Group"
            }
          },
          "meerkat_schema": {
            "sql_expression": "group_id",
            "type": "string"
          },
          "reference_name": "group_id"
        },
        {
          "devrev_schema": {
            "field_type": "timestamp",
            "is_filterable": true,
            "name": "record_date",
            "ui": {
              "display_name": "Range"
            }
          },
          "meerkat_schema": {
            "sql_expression": "record_date",
            "type": "time"
          },
          "reference_name": "record_date"
        },
        {
          "devrev_schema": {
            "field_type": "id",
            "id_type": [
              "part"
            ],
            "is_filterable": true,
            "name": "primary_part_id",
            "ui": {
              "display_name": "Part"
            }
          },
          "meerkat_schema": {
            "sql_expression": "primary_part_id",
            "type": "string"
          },
          "reference_name": "primary_part_id"
        },
        {
          "devrev_schema": {
            "allowed_values": [
              "active",
              "breached",
              "completed",
              "warning",
              "paused"
            ],
            "base_type": "enum",
            "field_type": "array",
            "is_filterable": true,
            "name": "sla_stage",
            "ui": {
              "display_name": "SLA Stage"
            }
          },
          "meerkat_schema": {
            "sql_expression": "sla_stage",
            "type": "string"
          },
          "reference_name": "sla_stage"
        },
        {
          "devrev_schema": {
            "field_type": "id",
            "id_type": [
              "dev_user",
              "rev_user"
            ],
            "is_filterable": true,
            "name": "Owner",
            "ui": {
              "display_name": "Owner"
            }
          },
          "meerkat_schema": {
            "sql_expression": "owned_by_ids",
            "type": "string_array"
          },
          "reference_name": "owned_by_ids"
        }
      ],
      "measures": [
        {
          "devrev_schema": {
            "field_type": "int",
            "is_filterable": true,
            "name": "unique_ids_count",
            "ui": {
              "display_name": "Tickets"
            }
          },
          "meerkat_schema": {
            "sql_expression": "COUNT(DISTINCT id)",
            "type": "number"
          },
          "reference_name": "unique_ids_count"
        }
      ],
      "oasis": {
        "datasets": [
          "system.support_insights_ticket_metrics_summary"
        ],
        "sql_query": "select record_hour AS record_date,* from system.support_insights_ticket_metrics_summary WHERE account_id IS NOT NULL AND account_id != '' AND state != 'closed'"
      },
      "reference_name": "support_insights_ticket_metrics_summary",
      "type": "oasis"
    }
  ]
```

Moreover, each object in the `data_sources` array above requires:

`type`: The source type, in this case, `oasis`
`reference_name`: Unique identifier used to reference this source
`oasis`: Configuration for oasis data
`dimensions`: Array of dimension definitions
`measures`: Array of measure definitions

The `data_sources` section is the foundation of your widget. It defines:

Datasets and base query
Dimensions and measures
Supported field types for dimensions/measures

## Datasets and Base Query

In the `oasis` section:

```json
"oasis": {
  "datasets": [
  // List of tables/datasets to use
    "system.dataset1",
    "system.dataset2"
  ],
    "sql_query": "Your base SQL query goes here"
}
```

Here, `datasets` include a list of all tables/views that your SQL query will use, i.e.
"system.dataset1",
"system.dataset2"
from the above. And,`sql_query` is base SQL query that joins and processes your data, i.e.
"sql_query": "Your base SQL query goes here"
from the above.

Example - Putting it all together:

```json
"oasis": {
  "datasets": [
    "system.support_insights_ticket_metrics_summary"
  ],
  "sql_query": "select record_hour AS record_date, \* from    system.support_insights_ticket_metrics_summary WHERE account_id IS NOT NULL AND account_id != '' AND state != 'closed'"\
```

For more information about the base query, see base-query.md file.

## Reference Names for Data Source

They must be unique within the widget
Should match the primary table/view name
Used to qualify all dimension and measure references

```json
{
  "type": "oasis",
  "reference_name": "your_source_name" // This name must be used to qualify fields
  // ... other configuration
}
```

## Dimensions

Dimensions represent filters of your base query. They are the categorical, non-numerical columns within the table.
They have the following values within them:

`field_type`: The type of field, i.e. id, timestamp, enum, bool, tokens, array
`db_name`: Database column name
`name`: Reference name for the field
`is_filterable`: Whether this field can be used as a filter
`ui`: Display settings for the field

Example dimension:

```json
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
```

## Measures

Measures define numerical columns within your base query. They are normally result sets of aggregate function in the base query.
Each measure includes the following values:

`field_type`: Data type (int, double, etc.)
`db_name`: Column name for the measure
`name`: Reference name
`ui`: Display settings
`sql_expression`: The aggregation function to apply

Example measure:

```json
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
```

## Field Types in Dimensions and Measures

When defining dimensions and measures, field types need to be defined.
These field types are native to DevRev, the company.
Here is a list of possible field type values for each type of variable.
Please look at the table schemas provided by the user to determine the best-fit field type below.
And pay particular attention to the notes below some of the categories below.

Numeric Types:

`int`: Integer values
`double`: Floating-point numbers
`decimal`: Precise decimal numbers
`currency`: Monetary values

Note: Use appropriate numeric types, i.e. `int`, `double`, `decimal` based on the precision of the values within the numerical column.

Boolean Type\*\*

`bool`: True/false values

Text Types

`string`: Basic string values
`text`: Longer text content
`tokens`: Tokenized text for search/filtering
`rich_text`: Formatted text with markup
`bytes`: Binary data

Note: Choose between text types based on the content within the column and requirements for searching through this data.

Time Type:

`timestamp`: Date and time values

Note: Use `timestamp` for all date/time fields.

Reference Types:

`id`: Unique identifiers
`overridable_enum`: Enumerated values that can be overridden
`uenum`: User-defined enumeration
`reference_enum`: Reference to enumerated values

Note: Select correct enumeration type, i.e. `overridable_enum`, `uenum`, `reference_enum` based on value source

Example of choosing field types for a dimension:

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

Note: Similar process for measures.

## Reference Names for Dimensions and Measures

Must include data source reference name
Format: `your_source_name.field_name`
Example: `your_source_name.your_dimension`

## Best Practices

Use meaningful names for dimensions and measures
In measures and dimensions, use direct column names
Include appropriate filters in dimensions
Consider performance implications of complex joins
Use appropriate field types for better UI interaction
Avoid table aliases in sql_expression fields
Use proper column qualification when names are ambiguous
