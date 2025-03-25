# Input

Given the base SQL query: SELECT \* FROM system.article_views_and_votes_summary s LEFT OUTER JOIN system.dim_article a ON s.article_id = a.id AND a.is_deleted != true And the table schema: article_views_and_votes_summary Schema article_id VARCHAR record_date DATE account_id VARCHAR surface VARCHAR is_verified BOOLEAN total_views BIGINT total_duration_ms BIGINT unique_views BIGINT article_upvotes BIGINT article_downvotes BIGINT dim_article Schema stock_schema_fragment_id VARCHAR object_version BIGINT last_system_modification_version BIGINT modified_date TIMESTAMP authored_by_ids VARCHAR[] sync_metadata VARCHAR created_date TIMESTAMP owned_by_ids VARCHAR[] shared_with VARCHAR extracted_content VARCHAR[] external_source_data VARCHAR created_by_id VARCHAR modified_by_id VARCHAR subtype VARCHAR resource_json VARCHAR object_type VARCHAR operation VARCHAR tags_json VARCHAR custom_schema_fragment_ids VARCHAR[] status VARCHAR num_downvotes BIGINT title VARCHAR rank VARCHAR custom_fields VARCHAR display_id VARCHAR scope VARCHAR access_level BIGINT num_upvotes BIGINT applies_to_part_ids VARCHAR[] aliases VARCHAR[] id VARCHAR is_deleted BOOLEAN parent VARCHAR description VARCHAR type BIGINT published_date TIMESTAMP language VARCHAR
Understand the widget building guide below fully for how to create a widget. Keep in mind the base query and table schema. Generate the JSON configuration for a widget of what to visualize + visualization type.

## Follow-Up

<paste widget preview error here>

# Output

## Fix 5 - Cheat Sheet

### Article Analysis - Total Views + Unique Views Stacked-Bar Graph

- Could NOT generate widget
  - Table name does not exist in system
    - This error was fixed in total views table example below, but not this one
    - gpt-4o kept asking to manually test the SQL query by finding the correct table name, which is not autonomous


Error: Catalog Error: Table with name article_views_and_votes_summary does not exist! Did you mean "pg_catalog.pg_views"? LINE 1: ...te, s.total_views, s.unique_views FROM system.article_views_and_votes_summary ... ^

### Article Analysis - Unique Views Line Graph

don:data:dvrv-us-1:devo/0:widget/WB5RuESbH8

- After fixing below errors one-by-one
- Created line graph widget successfully

Error: Catalog Error: Table with name dim_article does not exist! Did you mean "system.information_schema.tables"? LINE 1: ...ws_and_votes_summary s LEFT OUTER JOIN system.dim_article a ON s.article_id = ... ^

Error: Binder Error: Referenced table "s" not found! Candidate tables: "article_views_data" LINE 1: ...iews_data**record_date FROM (SELECT \*, s.record_date AS article_views_data**re... ^

### Article Analysis - Total Views Table

don:data:dvrv-us-1:devo/0:widget/QfkEwq02Ea

- After fixing below errors one-by-one
- Created table widget successfully

Error: Binder Error: Referenced table "s" not found! Candidate tables: "articles_view_data" LINE 1: ...icles_view_data**title FROM (SELECT \*, s.article_id AS articles_view_data**art... ^

Error: Binder Error: Referenced table "article_views_and_votes_summary" not found! Candidate tables: "articles_view_data" LINE 1: ...icles_view_data\_\_title FROM (SELECT \*, article_views_and_votes_summary.article... ^

Failed to create widget - Invalid field: is_compact

- Fixed all errors
- Created table widget successfully

Follow-up: Ask to update widget to line graph
