# Final Widget - Sample Template

NOTE: Ensure final JSON configuration format follows this sample template.
NOTE: Remove any added fields that are not mentioned within this guide.

```json
{
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
        "dimensions": ["support_insights_ticket_metrics_summary.account_id"],
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

NOTE: If widget is created successfully, but the visualization does not show, ask before assuming or changing base query or visualization type.
