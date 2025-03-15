# Sub-widgets

Sub-widgets define how to query and display your data.
They are composed of the query and visualization.

Example sub-widget:

```json
"sub_widgets": [
{
"query": {
"dimensions": [
"article_data.title"
],
"measures": [
"article_data.total_views",
"article_data.unique_views"
],
"order_by": [
{
"direction": "descending",
"reference_name": "article_data.total_views"
}
]
},
"reference_id": "article_table",
"visualization": {
"table": {
"columns": [
{
"label": "Article",
"reference_name": "article_data.title"
},
{
"label": "Total Views",
"reference_name": "article_data.total_views"
},
{
"label": "Unique Views",
"reference_name": "article_data.unique_views"
}
]
},
"type": "table"
}
}
]
```

## Query

The query contains corresponding dimensions and measures, as well as the ordering/grouping within the base query.
See the example below.

```json
"query": {
"dimensions": [
"article_data.title"
],
"measures": [
"article_data.total_views",
"article_data.unique_views"
],
"order_by": [
{
"direction": "descending",
"reference_name": "article_data.total_views"
}
]
}
```

Dimension and Measure References in Queries:

Every dimension and measure MUST be referenced with its data source name.
See example below:

```json
// 🚫 NEVER DO THIS:
"dimensions": ["dimension_name"]

// ✅ ALWAYS DO THIS:
"dimensions": ["data_source_name.dimension_name"]
```

Putting it together in the query:

```json
// INCORRECT - unqualified references
"query": {
  "dimensions": ["some_dimension"],
  "measures": ["some_measure"]
}

// CORRECT - fully qualified with data source
"query": {
  "dimensions": ["your_source_name.some_dimension"],
  "measures": ["your_source_name.some_measure"]
}
```

## Visualization

The second part of the sub-widget is the visualization.
The example below comes right after the `reference_id` field.

```json
      "visualization": {
        "table": {
          "columns": [
            {
              "label": "Article",
              "reference_name": "article_data.title"
            },
            {
              "label": "Total Views",
              "reference_name": "article_data.total_views"
            },
            {
              "label": "Unique Views",
              "reference_name": "article_data.unique_views"
            }
          ]
        },
        "type": "table"
      }
```

### Visualization Types

Common visualization types and use cases are below.

For tabular data, use `table`
Use `bar` for verticle or horizontal bar charts, comparing numerical data
`line` is best for Line graphs depicting numerical trends
For percentages, you can use `pie` or `donut`
The `packed_bubble` is primarily for hierarchical data, containing categoreis and sizes corresponding to the bubbles
For comparing more than two columns, i.e. multi-variate analysis, use a `heatmap`
To display single values, use `metric`

See below for examples of these structures within the visualization section.

Table:

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

NOTE: To enable GroupBy in Table add is_groupable in dimension
{ "ui": { "is_groupable": true } }

Line:

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

Bar/Horizontal Bar:

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
```

NOTE: is_stacked is optional and it is used when you have done group by twice

Column/Vertical bar chart)

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

NOTE 1: is_stacked MUST be optional and it is used when you have done group by twice
NOTE 2: This example is with stacked true and color object indicates which key to what color

Packed Bubble:

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

Donut:

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

Pie chart:

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

Heatmap:

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

Metric:

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
