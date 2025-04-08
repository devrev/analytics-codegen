# Dimensions / Measure

NOTE: Add only necessary dimensions/measures for widget here.
NOTE: Do not add any extra fields to devrev/meerkat schema that are not listed below.

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
List of valid ID types

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

## Formatters

Timestamp

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

Time duration
NOTE:- field_type can be int as well
NOTE:- unit is the input unit type of the data. Other possible

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
NOTE:- is_compact is used to see the compact version of the data like 100K,
1M

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
NOTE:- precision is used to provide how many digits you want to see after decimal point

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
