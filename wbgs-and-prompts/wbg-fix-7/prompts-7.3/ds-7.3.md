# Data Source

Data source should look like this:

```json
"data_sources": [
    {
      "dimensions": [
        {
          "devrev_schema": {
            "field_type": "id",
            "id_type": ["work"],
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
            "allowed_values": ["High", "Medium", "Low", "Blocker"],
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
            "id_type": ["account"],
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
            "id_type": ["rev_org"],
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
            "id_type": ["account"],
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
            "id_type": ["part"],
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
            "id_type": ["tag"],
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
            "id_type": ["group"],
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
            "id_type": ["part"],
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
            "id_type": ["dev_user", "rev_user"],
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
        "datasets": ["system.support_insights_ticket_metrics_summary"],
        "sql_query": "select record_hour AS record_date,* from system.support_insights_ticket_metrics_summary WHERE account_id IS NOT NULL AND account_id != '' AND state != 'closed'"
      },
      "reference_name": "support_insights_ticket_metrics_summary",
      "type": "oasis"
    }
  ]
```

## Dimensions / Measure

Add only necessary dimensions/measures for widget here.
Do not add any extra fields to devrev/meerkat schema that are not listed below.

enums

```json
{
  "devrev_schema": {
    "allowed_values": ["High", "Medium", "Low", "Blocker"],
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
}
```

Object Types
List of valid ID types:

```json
{
  "devrev_schema": {
    "field_type": "id",
    "id_type": ["work"],
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
}
```

Timestamp / Date

```json
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
}
```

Int

```json
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
```

Double

```json
{
  "devrev_schema": {
    "field_type": "double",
    "is_filterable": false,
    "name": "median_age",
    "ui": {
      "display_name": "Median Age"
    }
  },
  "meerkat_schema": {
    "sql_expression": "median(age)",
    "type": "number"
  },
  "reference_name": "median_age"
}
```

Text / string

```json
{
  "devrev_schema": {
    "field_type": "text",
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
}
```

### Formatters

#### Timestamp

Percentage
NOTE:- field_type can be int as well

```json
{
  "devrev_schema": {
    "field_type": "double",
    "name": "distinct_count",
    "ui": {
      "display_name": "Distinct Count",
      "unit": "percentage"
    }
  },
  "meerkat_schema": {
    "sql_expression": "100.0 * (COUNT(DISTINCT CASE WHEN severity_name = 'Blocker' AND state != 'closed' AND state IS NOT NULL THEN id END) / NULLIF(COUNT(DISTINCT CASE WHEN state != 'closed' AND state IS NOT NULL THEN id END), 0))",
    "type": "number"
  },
  "reference_name": "distinct_count"
}
```

Currency
NOTE:- field_type can be int as well
NOTE:- unit is used to define the currency type.

```json
{
  "devrev_schema": {
    "field_type": "double",
    "name": "opportunity_total_amount",
    "ui": {
      "display_name": "Pipeline Amount",
      "is_currency_field": true,
      "unit": "USD",
      "order": 1
    }
  },
  "meerkat_schema": {
    "sql_expression": "SUM(CASE WHEN state = 'open' OR state = 'in_progress' THEN (amount*fprobability/100) ELSE 0 END)",
    "type": "number"
  },
  "reference_name": "opportunity_total_amount"
}
```

#### Time duration

`field_type` can be int as well.
`unit` is the input unit type of the data. Others are possible.

```json
"milliseconds",
"seconds",
"minutes",
"hours",
"days"{
    "devrev_schema": {
        "field_type": "double",
        "is_filterable": false,
        "name": "median_diff_minutes",
        "ui": {
            "display_name": "Median resolution time",
            "unit": "minutes"
        }
    },
    "meerkat_schema": {
        "sql_expression": "MEDIAN(DATEDIFF('minute', created_date, actual_close_date))",
        "type": "number"
    },
    "reference_name": "median_diff_minutes"
}
```

Int
`is_compact` is used when data is large, i.e. 100K or 1M, to see the compact version of the data.

```json
{
  "devrev_schema": {
    "field_type": "int",
    "is_filterable": true,
    "name": "unique_ids_count",
    "ui": {
      "display_name": "Unique Ids Count",
      "is_compact": true
    }
  },
  "meerkat_schema": {
    "sql_expression": "COUNT(DISTINCT id)",
    "type": "number"
  },
  "reference_name": "unique_ids_count"
}
```

Double
`precision` dictates how many digits you want to see after decimal point.

```json
{
  "devrev_schema": {
    "field_type": "double",
    "is_filterable": true,
    "name": "unique_ids_count",
    "ui": {
      "display_name": "Unique Ids Count",
      "precision": 2
    }
  },
  "meerkat_schema": {
    "sql_expression": "COUNT(DISTINCT id)",
    "type": "number"
  },
  "reference_name": "unique_ids_count"
}
```
