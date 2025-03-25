# Input

Given the base SQL query:
SELECT id, created_date, mitigated_date, identified_date, actual_close_date, applies_to_part_ids AS part_ids, JSON_EXTRACT_STRING (stage_json, '$.stage_id') AS stage_id, state, JSON_EXTRACT_STRING (severity_json, '$.id') AS severity_id, owned_by_ids, JSON_EXTRACT_STRING (impact, '$.customer_ids[*]') AS impacted_customers FROM system.dim_incident

And the table schema: dim_incident
dim_incident

Schema
object_type VARCHAR
stock_schema_fragment VARCHAR
playbook_ids VARCHAR[]
subtype VARCHAR
stock_schema_fragment_id VARCHAR
mitigated_date TIMESTAMP
actual_close_date TIMESTAMP
severity_json VARCHAR
id VARCHAR
state VARCHAR
resolved_at TIMESTAMP
custom_fields VARCHAR
pia_ids VARCHAR[]
stakeholders VARCHAR[]
stage_json VARCHAR
operation VARCHAR
modified_date TIMESTAMP
display_id VARCHAR
applies_to_part_ids VARCHAR[]
artifact_ids VARCHAR[]
impact VARCHAR
acknowledged_date TIMESTAMP
identified_at TIMESTAMP
source VARCHAR
modified_by_id VARCHAR
body VARCHAR
object_version BIGINT
tags_json VARCHAR
created_by_id VARCHAR
custom_schema_fragments VARCHAR[]
owned_by_ids VARCHAR[]
identified_date TIMESTAMP
is_deleted BOOLEAN
title VARCHAR
last_system_modification_version BIGINT
impacted_customers VARCHAR[]
target_close_date TIMESTAMP
created_date TIMESTAMP
reported_by VARCHAR
custom_schema_fragment_ids VARCHAR[]
related_doc_ids VARCHAR[]

Understand the widget building guide below fully for how to create a widget. Keep in mind the base query and table schema. Generate the JSON configuration for a widget of incident count in a column chart.

# Follow-Up

 <paste error here>

# Trials

## Fix 6 - Instructions + Code

Successful: after one error - wrong config value!

don:data:dvrv-us-1:devo/0:widget/BwgMT9VMEd

- Column chart of total incidents

CONVO:

Failed to create widget - Invalid field: is_compact
