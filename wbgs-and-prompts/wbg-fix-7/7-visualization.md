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
