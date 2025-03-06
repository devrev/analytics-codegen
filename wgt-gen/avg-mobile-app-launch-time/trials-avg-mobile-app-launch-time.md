### Input

Base query:
SELECT network_operator, app_launch_time FROM system.mobile_sessions_metadatas_v1

Schema:
mobile_sessions_metadatas_v1
Schema
session_id
session_id
VARCHAR
created_at
TIMESTAMP
version_key
VARCHAR
identifier
VARCHAR
network_operator
VARCHAR
network_type
VARCHAR
first_user_interaction
BIGINT
app_launch_time
BIGINT
app_launch_type
VARCHAR
device_manufacturer
VARCHAR
device_name
VARCHAR
app_version
VARCHAR
exception_type
VARCHAR
error_count
BIGINT
is_rage
BIGINT
ux_evaluation
VARCHAR
platform
VARCHAR
According to the widget-building guide, base query and table schemas, generate a JSON file for the widget.

### Output

#### Fix 1 - Field Types

Error: Failed to create widget - Invalid field: x_axis

- Note: Got same error for original (see above)
  - Earlier trial of same JSON files, x-axis error was not caught

#### Original

Error: Failed to create widget - Missing required field: allowed_values
