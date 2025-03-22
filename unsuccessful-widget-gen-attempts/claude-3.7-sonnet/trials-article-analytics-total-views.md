# Input

You are going to be an expert at generating a widget, given the following information.

First, this is the base SQL query you need to know:

SELECT \* FROM system.article_views_and_votes_summary s LEFT OUTER JOIN system.dim_article a ON s.article_id = a.id AND a.is_deleted != true

Then, there's the table schema:

article_views_and_votes_summary

Schema

article_id VARCHAR

record_date DATE

account_id VARCHAR

surface VARCHAR

is_verified BOOLEAN

total_views BIGINT

total_duration_ms BIGINT

unique_views BIGINT

article_upvotes BIGINT

article_downvotes BIGINT

dim_article

Schema

stock_schema_fragment_id VARCHAR

object_version BIGINT

last_system_modification_version BIGINT

modified_date TIMESTAMP

authored_by_ids VARCHAR[]

sync_metadata VARCHAR

created_date TIMESTAMP

owned_by_ids VARCHAR[]

shared_with VARCHAR

extracted_content VARCHAR[]

external_source_data VARCHAR

created_by_id VARCHAR

modified_by_id VARCHAR

subtype VARCHAR

resource_json VARCHAR

object_type VARCHAR

operation VARCHAR

tags_json VARCHAR

custom_schema_fragment_ids VARCHAR[]

status VARCHAR

num_downvotes BIGINT

title VARCHAR

rank VARCHAR

custom_fields VARCHAR

display_id VARCHAR

scope VARCHAR

access_level BIGINT

num_upvotes BIGINT

applies_to_part_ids VARCHAR[]

aliases VARCHAR[]

id VARCHAR

is_deleted BOOLEAN

parent VARCHAR

description VARCHAR

type BIGINT

published_date TIMESTAMP

language VARCHAR

#File:#Folder:

Understand the widget building guide attached fully for how to create a widget. Keep in mmind the base query and table(s) schema for widget creation. Plese provide the correct JSON file.

## Follow-Up - Errors

<error message from widget-preview>

# Output

#### Fix 4 - Data Source

Expected property name or '}' in JSON at position 4 (line 2 column 3)

- Need to remove {} around data source object

Error: Binder Error: Referenced column "article_views_and_votes_summary**record_date" not found in FROM clause! Candidate bindings: "article_analytics.article_downvotes" LINE 1: ...alytics) AS article_analytics GROUP BY article_views_and_votes_summary**record... ^

- SQL query error

#### Fix 3 - Specific Instructions + Splitting Files

Failed to create widget - unexpected discriminator: strin
Unterminated string in JSON at position 2844 (line 111 column 17)

- Looped to same error
  Error: Binder Error: Referenced column "article_data**title" not found in FROM clause! Candidate bindings: "article_data.title" LINE 1: ...article_data) AS article_data GROUP BY article_data**title ORDER BY article_da... ^
- Need to primarily fix: Failed to create widget - unexpected discriminator: string

#### Fix 2 - Visualization + Errors

Failed to create widget - unexpected discriminator: string

- Upon follow-up question to fix JSON
  - Provided correct result! (See file)

#### Fix 1 - Field Types

Failed to create widget - Missing required field: reference_name

- No change

#### Original

Failed to create widget - Missing required field: reference_name
