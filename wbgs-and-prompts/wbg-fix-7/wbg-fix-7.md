# Widget Building Guide

## Initial Widget - Sample Template

NOTE: Initially, the widget configuration should look like this:

```json
{
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
    ],
    "description": "A list of your customers and the number of tickets they created, ranked from high to low.",
    "layout": [
        {
            "position": {
                "height": 1,
                "width": 1,
                "x": 0,
                "y": 0
            },
            "reference_id": "subwidget1"
        }
    ],
    "sub_widgets": [
        {
            "query": {
                "dimensions": [
                    "support_insights_ticket_metrics_summary.account_id"
                ],
                "measures": [
                    "support_insights_ticket_metrics_summary.unique_ids_count"
                ],
                "order_by": [
                    {
                        "direction": "descending",
                        "reference_name": "support_insights_ticket_metrics_summary.unique_ids_count"
                    }
                ]
            },
            "reference_id": "subwidget1",
            "visualization": {
                "table": {
                    "columns": [
                        {
                            "drill_throughs": [
                                {
                                    "dashboard": "don:data:dvrv-global:dashboard/dn7qoVCoiD",
                                    "label": "drill"
                                }
                            ],
                            "label": "Account",
                            "reference_name": "support_insights_ticket_metrics_summary.account_id"
                        },
                        {
                            "label": "Count",
                            "reference_name": "support_insights_ticket_metrics_summary.unique_ids_count"
                        }
                    ]
                },
                "type": "table"
            }
        }
    ],
    "title": "Customer Impact"
}
```

## Create Widget

### Dimensions / Measure

enums

```json
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
}
```

Object Types
List of valid ID types

```json
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

### Visualization

Table
NOTE: Choose when there are a lot of columns to display.

```json
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
```

To enable GroupBy in Table add is_groupable in dimension

```json
{
    "ui": {
        "is_groupable": true
    }
}
```

NOTE: Line, Bar, Column, PackedBubble, Donut, Pie and Heatmap are not supported for a lot of columns. Use Table instead.

Line
````json`
"visualization": {
    "line": {
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
    "type": "line"
}

````

Bar (Horizontal bar chart)
NOTE: is_stacked is optional and it is used when you have done group by twice
```json
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
````

Column (Vertical bar chart)
NOTE: is_stacked is optional and it is used when you have done group by twice
NOTE: This example is with stacked true and color object indicates which key to what color

```json
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
```

PackedBubble

```json
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
```

Donut

```json
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
```

Pie

```json
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
```

Heatmap

```json
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
```

Metric

NOTE: This is used when you want to show a single value.

```json
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
```

### Formatters

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

## Final Widget - Sample Template

NOTE: Ensure final JSON configuration format follows this sample template:

```json
{
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
    ],
    "description": "A list of your customers and the number of tickets they created, ranked from high to low.",
    "layout": [
        {
            "position": {
                "height": 1,
                "width": 1,
                "x": 0,
                "y": 0
            },
            "reference_id": "subwidget1"
        }
    ],
    "sub_widgets": [
        {
            "query": {
                "dimensions": [
                    "support_insights_ticket_metrics_summary.account_id"
                ],
                "measures": [
                    "support_insights_ticket_metrics_summary.unique_ids_count"
                ],
                "order_by": [
                    {
                        "direction": "descending",
                        "reference_name": "support_insights_ticket_metrics_summary.unique_ids_count"
                    }
                ]
            },
            "reference_id": "subwidget1",
            "visualization": {
                "table": {
                    "columns": [
                        {
                            "drill_throughs": [
                                {
                                    "dashboard": "don:data:dvrv-global:dashboard/dn7qoVCoiD",
                                    "label": "drill"
                                }
                            ],
                            "label": "Account",
                            "reference_name": "support_insights_ticket_metrics_summary.account_id"
                        },
                        {
                            "label": "Count",
                            "reference_name": "support_insights_ticket_metrics_summary.unique_ids_count"
                        }
                    ]
                },
                "type": "table"
            }
        }
    ],
    "title": "Customer Impact"
}
```
