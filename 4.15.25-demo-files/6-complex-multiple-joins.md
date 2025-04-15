# Input 1

Given the table schema:
Table name: system.article_views_and_votes_summary
Table schema: article_id VARCHAR record_date DATE account_id VARCHAR surface VARCHAR is_verified BOOLEAN total_views BIGINT total_duration_ms BIGINT unique_views BIGINT article_upvotes BIGINT article_downvotes BIGINT
Table name: system.dim_article
Table schema: stock_schema_fragment_id VARCHAR object_version BIGINT last_system_modification_version BIGINT modified_date TIMESTAMP authored_by_ids VARCHAR[] sync_metadata VARCHAR created_date TIMESTAMP owned_by_ids VARCHAR[] shared_with VARCHAR extracted_content VARCHAR[] external_source_data VARCHAR created_by_id VARCHAR modified_by_id VARCHAR subtype VARCHAR resource_json VARCHAR object_type VARCHAR operation VARCHAR tags_json VARCHAR custom_schema_fragment_ids VARCHAR[] status VARCHAR num_downvotes BIGINT title VARCHAR rank VARCHAR custom_fields VARCHAR display_id VARCHAR scope VARCHAR access_level BIGINT num_upvotes BIGINT applies_to_part_ids VARCHAR[] aliases VARCHAR[] id VARCHAR is_deleted BOOLEAN parent VARCHAR description VARCHAR type BIGINT published_date TIMESTAMP language VARCHAR
Generate an appropriate SQL query for a widget of
total article views
in a
line graph.

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
Table name: system.article_views_and_votes_summary
Table schema: article_id VARCHAR record_date DATE account_id VARCHAR surface VARCHAR is_verified BOOLEAN total_views BIGINT total_duration_ms BIGINT unique_views BIGINT article_upvotes BIGINT article_downvotes BIGINT
Table name: system.dim_article
Table schema: stock_schema_fragment_id VARCHAR object_version BIGINT last_system_modification_version BIGINT modified_date TIMESTAMP authored_by_ids VARCHAR[] sync_metadata VARCHAR created_date TIMESTAMP owned_by_ids VARCHAR[] shared_with VARCHAR extracted_content VARCHAR[] external_source_data VARCHAR created_by_id VARCHAR modified_by_id VARCHAR subtype VARCHAR resource_json VARCHAR object_type VARCHAR operation VARCHAR tags_json VARCHAR custom_schema_fragment_ids VARCHAR[] status VARCHAR num_downvotes BIGINT title VARCHAR rank VARCHAR custom_fields VARCHAR display_id VARCHAR scope VARCHAR access_level BIGINT num_upvotes BIGINT applies_to_part_ids VARCHAR[] aliases VARCHAR[] id VARCHAR is_deleted BOOLEAN parent VARCHAR description VARCHAR type BIGINT published_date TIMESTAMP language VARCHAR
For a widget of
total article views
in a
line graph
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
