# Input

Given the base SQL query: SELECT \* FROM system.article_views_and_votes_summary s LEFT OUTER JOIN system.dim_article a ON s.article_id = a.id AND a.is_deleted != true And the table schema: article_views_and_votes_summary Schema article_id VARCHAR record_date DATE account_id VARCHAR surface VARCHAR is_verified BOOLEAN total_views BIGINT total_duration_ms BIGINT unique_views BIGINT article_upvotes BIGINT article_downvotes BIGINT dim_article Schema stock_schema_fragment_id VARCHAR object_version BIGINT last_system_modification_version BIGINT modified_date TIMESTAMP authored_by_ids VARCHAR[] sync_metadata VARCHAR created_date TIMESTAMP owned_by_ids VARCHAR[] shared_with VARCHAR extracted_content VARCHAR[] external_source_data VARCHAR created_by_id VARCHAR modified_by_id VARCHAR subtype VARCHAR resource_json VARCHAR object_type VARCHAR operation VARCHAR tags_json VARCHAR custom_schema_fragment_ids VARCHAR[] status VARCHAR num_downvotes BIGINT title VARCHAR rank VARCHAR custom_fields VARCHAR display_id VARCHAR scope VARCHAR access_level BIGINT num_upvotes BIGINT applies_to_part_ids VARCHAR[] aliases VARCHAR[] id VARCHAR is_deleted BOOLEAN parent VARCHAR description VARCHAR type BIGINT published_date TIMESTAMP language VARCHAR Understand the widget building guide below fully for how to create a widget. Keep in mind the base query and table schema. Generate the JSON configuration for a stacked-bar graph of upvotes vs. downvotes.

# Follow-Up

<Paste error here>

# Output

## Fix 7 Stacked Bar Graph - Upvotes vs. Downvotes

IDs:
don:data:dvrv-us-1:devo/0:widget/kOH3J7se9U

- Incorrectly displayed

don:data:dvrv-us-1:devo/0:widget/KFb7KlMFHb

- Vertical bar, successful!

don:data:dvrv-us-1:devo/0:widget/QdcXXJ67Ee

- Horizontal bar, successful!

Error: Binder Error: Referenced table "a" not found! Candidate tables: "article_votes" LINE 1: ... article_votes**title FROM (SELECT \*, a.title AS article_votes**title FROM (S... ^

Error: Binder Error: column "article_upvotes" must appear in the GROUP BY clause or must be part of an aggregate function. Either add it to the GROUP BY list, or use "ANY_VALUE(article_upvotes)" if the exact value of "article_upvotes" is not important. LINE 1: SELECT COALESCE(article_upvotes, 0) AS article_votes\_\_a... ^
