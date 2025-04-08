# Widget Generation

## Input: Total Article Views

Given the base SQL query: SELECT \* FROM system.article_views_and_votes_summary s LEFT OUTER JOIN system.dim_article a ON s.article_id = a.id AND a.is_deleted != true And the table schema: article_views_and_votes_summary Schema article_id VARCHAR record_date DATE account_id VARCHAR surface VARCHAR is_verified BOOLEAN total_views BIGINT total_duration_ms BIGINT unique_views BIGINT article_upvotes BIGINT article_downvotes BIGINT dim_article Schema stock_schema_fragment_id VARCHAR object_version BIGINT last_system_modification_version BIGINT modified_date TIMESTAMP authored_by_ids VARCHAR[] sync_metadata VARCHAR created_date TIMESTAMP owned_by_ids VARCHAR[] shared_with VARCHAR extracted_content VARCHAR[] external_source_data VARCHAR created_by_id VARCHAR modified_by_id VARCHAR subtype VARCHAR resource_json VARCHAR object_type VARCHAR operation VARCHAR tags_json VARCHAR custom_schema_fragment_ids VARCHAR[] status VARCHAR num_downvotes BIGINT title VARCHAR rank VARCHAR custom_fields VARCHAR display_id VARCHAR scope VARCHAR access_level BIGINT num_upvotes BIGINT applies_to_part_ids VARCHAR[] aliases VARCHAR[] id VARCHAR is_deleted BOOLEAN parent VARCHAR description VARCHAR type BIGINT published_date TIMESTAMP language VARCHAR Understand the widget building guide below fully for how to create a widget. Keep in mind the base query and table schema. Generate the JSON configuration for a widget of total article views in a line graph.

## Input: Unique Article Views

Given the base SQL query: SELECT \* FROM system.article_views_and_votes_summary s LEFT OUTER JOIN system.dim_article a ON s.article_id = a.id AND a.is_deleted != true And the table schema: article_views_and_votes_summary Schema article_id VARCHAR record_date DATE account_id VARCHAR surface VARCHAR is_verified BOOLEAN total_views BIGINT total_duration_ms BIGINT unique_views BIGINT article_upvotes BIGINT article_downvotes BIGINT dim_article Schema stock_schema_fragment_id VARCHAR object_version BIGINT last_system_modification_version BIGINT modified_date TIMESTAMP authored_by_ids VARCHAR[] sync_metadata VARCHAR created_date TIMESTAMP owned_by_ids VARCHAR[] shared_with VARCHAR extracted_content VARCHAR[] external_source_data VARCHAR created_by_id VARCHAR modified_by_id VARCHAR subtype VARCHAR resource_json VARCHAR object_type VARCHAR operation VARCHAR tags_json VARCHAR custom_schema_fragment_ids VARCHAR[] status VARCHAR num_downvotes BIGINT title VARCHAR rank VARCHAR custom_fields VARCHAR display_id VARCHAR scope VARCHAR access_level BIGINT num_upvotes BIGINT applies_to_part_ids VARCHAR[] aliases VARCHAR[] id VARCHAR is_deleted BOOLEAN parent VARCHAR description VARCHAR type BIGINT published_date TIMESTAMP language VARCHAR Understand the widget building guide below fully for how to create a widget. Keep in mind the base query and table schema. Generate the JSON configuration for a widget of unique article views in a line graph.

## Input: Upvotes vs. Downvotes

Given the base SQL query: SELECT \* FROM system.article_views_and_votes_summary s LEFT OUTER JOIN system.dim_article a ON s.article_id = a.id AND a.is_deleted != true And the table schema: article_views_and_votes_summary Schema article_id VARCHAR record_date DATE account_id VARCHAR surface VARCHAR is_verified BOOLEAN total_views BIGINT total_duration_ms BIGINT unique_views BIGINT article_upvotes BIGINT article_downvotes BIGINT dim_article Schema stock_schema_fragment_id VARCHAR object_version BIGINT last_system_modification_version BIGINT modified_date TIMESTAMP authored_by_ids VARCHAR[] sync_metadata VARCHAR created_date TIMESTAMP owned_by_ids VARCHAR[] shared_with VARCHAR extracted_content VARCHAR[] external_source_data VARCHAR created_by_id VARCHAR modified_by_id VARCHAR subtype VARCHAR resource_json VARCHAR object_type VARCHAR operation VARCHAR tags_json VARCHAR custom_schema_fragment_ids VARCHAR[] status VARCHAR num_downvotes BIGINT title VARCHAR rank VARCHAR custom_fields VARCHAR display_id VARCHAR scope VARCHAR access_level BIGINT num_upvotes BIGINT applies_to_part_ids VARCHAR[] aliases VARCHAR[] id VARCHAR is_deleted BOOLEAN parent VARCHAR description VARCHAR type BIGINT published_date TIMESTAMP language VARCHAR Understand the widget building guide below fully for how to create a widget. Keep in mind the base query and table schema. Generate the JSON configuration for a widget of upvotes vs. downvotes in a stacked-bar graph.

## Follow-Up

<paste widget preview error here>

# Base Query Generation

## Input: Total Article Views

Given the table schema: article_views_and_votes_summary Schema article_id VARCHAR record_date DATE account_id VARCHAR surface VARCHAR is_verified BOOLEAN total_views BIGINT total_duration_ms BIGINT unique_views BIGINT article_upvotes BIGINT article_downvotes BIGINT dim_article Schema stock_schema_fragment_id VARCHAR object_version BIGINT last_system_modification_version BIGINT modified_date TIMESTAMP authored_by_ids VARCHAR[] sync_metadata VARCHAR created_date TIMESTAMP owned_by_ids VARCHAR[] shared_with VARCHAR extracted_content VARCHAR[] external_source_data VARCHAR created_by_id VARCHAR modified_by_id VARCHAR subtype VARCHAR resource_json VARCHAR object_type VARCHAR operation VARCHAR tags_json VARCHAR custom_schema_fragment_ids VARCHAR[] status VARCHAR num_downvotes BIGINT title VARCHAR rank VARCHAR custom_fields VARCHAR display_id VARCHAR scope VARCHAR access_level BIGINT num_upvotes BIGINT applies_to_part_ids VARCHAR[] aliases VARCHAR[] id VARCHAR is_deleted BOOLEAN parent VARCHAR description VARCHAR type BIGINT published_date TIMESTAMP language VARCHAR and the prompt for base query generation below, fully understand the pormpt and table schema. Generate an appropirate SQL query for a widget of total article views in a line graph.

## Input: Unique Article Views

Given the table schema: article_views_and_votes_summary Schema article_id VARCHAR record_date DATE account_id VARCHAR surface VARCHAR is_verified BOOLEAN total_views BIGINT total_duration_ms BIGINT unique_views BIGINT article_upvotes BIGINT article_downvotes BIGINT dim_article Schema stock_schema_fragment_id VARCHAR object_version BIGINT last_system_modification_version BIGINT modified_date TIMESTAMP authored_by_ids VARCHAR[] sync_metadata VARCHAR created_date TIMESTAMP owned_by_ids VARCHAR[] shared_with VARCHAR extracted_content VARCHAR[] external_source_data VARCHAR created_by_id VARCHAR modified_by_id VARCHAR subtype VARCHAR resource_json VARCHAR object_type VARCHAR operation VARCHAR tags_json VARCHAR custom_schema_fragment_ids VARCHAR[] status VARCHAR num_downvotes BIGINT title VARCHAR rank VARCHAR custom_fields VARCHAR display_id VARCHAR scope VARCHAR access_level BIGINT num_upvotes BIGINT applies_to_part_ids VARCHAR[] aliases VARCHAR[] id VARCHAR is_deleted BOOLEAN parent VARCHAR description VARCHAR type BIGINT published_date TIMESTAMP language VARCHAR and the prompt for base query generation below, fully understand the pormpt and table schema. Generate an appropirate SQL query for a widget of unique article views in a line graph.

## Input: Upvotes vs. Downvotes

Given the table schema: article_views_and_votes_summary Schema article_id VARCHAR record_date DATE account_id VARCHAR surface VARCHAR is_verified BOOLEAN total_views BIGINT total_duration_ms BIGINT unique_views BIGINT article_upvotes BIGINT article_downvotes BIGINT dim_article Schema stock_schema_fragment_id VARCHAR object_version BIGINT last_system_modification_version BIGINT modified_date TIMESTAMP authored_by_ids VARCHAR[] sync_metadata VARCHAR created_date TIMESTAMP owned_by_ids VARCHAR[] shared_with VARCHAR extracted_content VARCHAR[] external_source_data VARCHAR created_by_id VARCHAR modified_by_id VARCHAR subtype VARCHAR resource_json VARCHAR object_type VARCHAR operation VARCHAR tags_json VARCHAR custom_schema_fragment_ids VARCHAR[] status VARCHAR num_downvotes BIGINT title VARCHAR rank VARCHAR custom_fields VARCHAR display_id VARCHAR scope VARCHAR access_level BIGINT num_upvotes BIGINT applies_to_part_ids VARCHAR[] aliases VARCHAR[] id VARCHAR is_deleted BOOLEAN parent VARCHAR description VARCHAR type BIGINT published_date TIMESTAMP language VARCHAR and the prompt for base query generation below, fully understand the pormpt and table schema. Generate an appropirate SQL query for a widget of upvotes vs. downvotes in a stacked-bar graph.

# Output

## Fix 7.2 - Base query

### Unique Views

QUERY GEN:
SELECT article_views_and_votes_summary.article_id, article_views_and_votes_summary.record_date, article_views_and_votes_summary.unique_views FROM article_views_and_votes_summary WHERE article_views_and_votes_summary.article_id IS NOT NULL AND article_views_and_votes_summary.record_date IS NOT NULL AND article_views_and_votes_summary.unique_views IS NOT NULL AND article_views_and_votes_summary.unique_views > 0 ORDER BY article_views_and_votes_summary.record_date

ERRORS:
Request failed with status code 404

RESULT:
Roadblock - Unable to fix 404 error 4 times; changed config to table unnecessarily.

### Upvotes vs. Downvotes

QUERY GEN:
SELECT dim_article.title, article_views_and_votes_summary.article_upvotes, article_views_and_votes_summary.article_downvotes FROM dim_article JOINarticle_views_and_votes_summary ON article_views_and_votes_summary.article_id = dim_article.id WHERE article_views_and_votes_summary.article_upvotes IS NOT NULL AND article_views_and_votes_summary.article_downvotes IS NOT NULL AND article_views_and_votes_summary.article_upvotes >= 0 AND article_views_and_votes_summary.article_downvotes >= 0 AND dim_article.is_deleted = FALSE

ERRORS:
Request failed with status code 404

RESULT:
Roadblock - Unable to fix 404 error 3 times; does not display.

## Fix 7 - More instructions

### Total Views

WGT ID:
don:data:dvrv-us-1:devo/0:widget/kfa5QzOzvT

ERRORS:
Failed to create wiedget - invalid type: is_compact

RESULT:
Success - Added base query prompt, see wbg-fix-7.md

### Unique Views

WGT ID:
don:data:dvrv-us-1:devo/0:widget/UgrmUVwxoC

ERRORS:
Failed to create wiedget - invalid type: is_compact

RESULT:
Success - Added base query prompt, see wbg-fix-7.md

### Upvotes vs. Downvotes

WGT ID:
<NONE>

ERRORS:
Error: Binder Error: Referenced column "article_upvotes" not found in FROM clause! Candidate bindings: "article_votes.total_upvotes" LINE 1: SELECT SUM(COALESCE(article_upvotes, 0)) AS article_votes\_\_... ^

Error: Binder Error: Referenced table "s" not found! Candidate tables: "article_votes" LINE 1: SELECT SUM(COALESCE(s.article_upvotes, 0)) AS article_votes... ^

RESULT:
Roadblock -Too many base query errors

## Fix 6 - Code + Instructions

### Unique Views Line Graph

ID:

don:data:dvrv-us-1:devo/0:widget/xJsjnlct4R

- Unique Views Over Time - Line Graph

CONVO:

Error: Binder Error: Referenced table "s" not found! Candidate tables: "article*views" LINE 1: ...cle_views**record_date FROM (SELECT \*, s.record_date AS article_views**record*... ^

- Just like before -> see below

Failed to create widget - Invalid field: is_compact

- Just like before -> see below

Widget Created Successfully!

- Just like before -> see below
  - After only 2 errors

### Total Views Line Graph

ID:
don:data:dvrv-us-1:devo/0:widget/6dGrrQVEiD

- Total Views Over Time - Line Graph

CONVO:

Error: Binder Error: Referenced table "s" not found! Candidate tables: "article_views_data" LINE 1: ...iews_data**record_date FROM (SELECT \*, s.record_date AS article_views_data**re... ^

- Just like before -> see below

Failed to create widget - Invalid field: is_compact

- Just like before -> see below

Widget Created Successfully!

- After only 2 errors!
  - Need to modify in following prompt, fix-7

### Top 10 Total Views Column Chart

don:data:dvrv-us-1:devo/0:widget/b556DCvnrJ

- Total views table: NOT a bar graph, but produced by model

don:data:dvrv-us-1:devo/0:widget/SsnyslLDac

- Top 10 Total views - column chart

CONVO:

Failed to create widget - Invalid field: is_compact

- Removed field, got another error...

Error: Binder Error: Referenced table "s" not found! Candidate tables: "article*views" LINE 1: ... article_views**title FROM (SELECT \*, s.record_date AS article_views**record*... ^

- Identified correct issue in SQL query
  - Changed table aliases accordingly!

Widget craeted successfully, but not displayed

- Conerts config to table for better data handling

Could you convert into a column chart?

- Successfuly creates column widget!
  - But uses top 10 values--good call, since all values are too much/do not display
    - Successfully follows modified instructions from fix 5 in wbg!

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
