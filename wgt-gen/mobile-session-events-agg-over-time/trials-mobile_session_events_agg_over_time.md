### Input

Base query:
SELECT created_at, event_count FROM system.mobile_sessions_events_agg ORDER BY created_at

Schema:
mobile_sessions_events_agg

Schema
app_version
VARCHAR
created_at
TIMESTAMP
version_key
VARCHAR
screen_name
VARCHAR
event_type_name
VARCHAR
crash_type
VARCHAR
exception_type
VARCHAR
event_count
BIGINT

According to the widget-building guide, base query and table schemas, generate a JSON file for the widget.

### Output

#### Fix 1 - Field Types

Error: Failed to create widget - Missing required field: reference_name

- Same as above (Original)

#### Original

Error: Failed to create widget - Missing required field: reference_name
