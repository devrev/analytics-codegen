# Input 1

Given the table schema:
Table name:
system.dim_incident
Table Schema: object_type VARCHAR stock_schema_fragment VARCHAR playbook_ids VARCHAR[] subtype VARCHAR stock_schema_fragment_id VARCHAR mitigated_date TIMESTAMP actual_close_date TIMESTAMP severity_json VARCHAR id VARCHAR state VARCHAR resolved_at TIMESTAMP custom_fields VARCHAR pia_ids VARCHAR[] stakeholders VARCHAR[] stage_json VARCHAR operation VARCHAR modified_date TIMESTAMP display_id VARCHAR applies_to_part_ids VARCHAR[] artifact_ids VARCHAR[] impact VARCHAR acknowledged_date TIMESTAMP identified_at TIMESTAMP source VARCHAR modified_by_id VARCHAR body VARCHAR object_version BIGINT tags_json VARCHAR created_by_id VARCHAR custom_schema_fragments VARCHAR[] owned_by_ids VARCHAR[] identified_date TIMESTAMP is_deleted BOOLEAN title VARCHAR last_system_modification_version BIGINT impacted_customers VARCHAR[] target_close_date TIMESTAMP created_date TIMESTAMP reported_by VARCHAR custom_schema_fragment_ids VARCHAR[] related_doc_ids VARCHAR[]
Generate an appropriate SQL query for a widget of
in progress vs. closed incident count per month
in a
bar graph.

## Data Source

Generate the data source for this query, given the following guide:
<insert data source guide here>

## Visualization

Generate the visualizatino for the widget, given the guide below:
<insert visualization guide here>

## Widget Building Guide

Finally, generate the complete widget configuration, given the widget-building guide below:
<insert widget-building guide here>

# Input 2

Given the table schema:
Table name:
system.dim_incident
Table Schema: object_type VARCHAR stock_schema_fragment VARCHAR playbook_ids VARCHAR[] subtype VARCHAR stock_schema_fragment_id VARCHAR mitigated_date TIMESTAMP actual_close_date TIMESTAMP severity_json VARCHAR id VARCHAR state VARCHAR resolved_at TIMESTAMP custom_fields VARCHAR pia_ids VARCHAR[] stakeholders VARCHAR[] stage_json VARCHAR operation VARCHAR modified_date TIMESTAMP display_id VARCHAR applies_to_part_ids VARCHAR[] artifact_ids VARCHAR[] impact VARCHAR acknowledged_date TIMESTAMP identified_at TIMESTAMP source VARCHAR modified_by_id VARCHAR body VARCHAR object_version BIGINT tags_json VARCHAR created_by_id VARCHAR custom_schema_fragments VARCHAR[] owned_by_ids VARCHAR[] identified_date TIMESTAMP is_deleted BOOLEAN title VARCHAR last_system_modification_version BIGINT impacted_customers VARCHAR[] target_close_date TIMESTAMP created_date TIMESTAMP reported_by VARCHAR custom_schema_fragment_ids VARCHAR[] related_doc_ids VARCHAR[]
For a widget of
in progress vs. closed incident count per month
in a
bar graph
Generate the SQL query, the data source (@ds.md), visualization (@vsl.md), and widget configuration (@wbg.md) with these files.
<insert ds.md>
<insert vsl.md>
<insert wbg.md>

# Follow-Up

## If Errors

<paste errors here, until resolved; cap = 10>

## If No Display

Widget did not display.

Widget Created Successfully! But does not display.

## Update Visualization

Can you change to a
<visualization type>?
