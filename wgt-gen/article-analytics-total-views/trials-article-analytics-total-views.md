### Input

#### Prompt

This is the base query:
SELECT \* FROM system.article_views_and_votes_summary s LEFT OUTER JOIN system.dim_article a ON s.article_id = a.id AND a.is_deleted != true

Here is the schema:
article_views_and_votes_summary

Schema
article_id
VARCHAR
record_date
DATE
account_id
VARCHAR
surface
VARCHAR
is_verified
BOOLEAN
total_views
BIGINT
total_duration_ms
BIGINT
unique_views
BIGINT
article_upvotes
BIGINT
article_downvotes
BIGINT

dim_article

Schema
stock_schema_fragment_id
VARCHAR
object_version
BIGINT
last_system_modification_version
BIGINT
modified_date
TIMESTAMP
authored_by_ids
VARCHAR[]
sync_metadata
VARCHAR
created_date
TIMESTAMP
owned_by_ids
VARCHAR[]
shared_with
VARCHAR
extracted_content
VARCHAR[]
external_source_data
VARCHAR
created_by_id
VARCHAR
modified_by_id
VARCHAR
subtype
VARCHAR
resource_json
VARCHAR
object_type
VARCHAR
operation
VARCHAR
tags_json
VARCHAR
custom_schema_fragment_ids
VARCHAR[]
status
VARCHAR
num_downvotes
BIGINT
title
VARCHAR
rank
VARCHAR
custom_fields
VARCHAR
display_id
VARCHAR
scope
VARCHAR
access_level
BIGINT
num_upvotes
BIGINT
applies_to_part_ids
VARCHAR[]
aliases
VARCHAR[]
id
VARCHAR
is_deleted
BOOLEAN
parent
VARCHAR
description
VARCHAR
type
BIGINT
published_date
TIMESTAMP
language
VARCHAR

Understand the file attached fully for how to build a widget. Provide a JSON file to generate a visualization, according to the base query, table schemas and attached guide above.

#### Follow-Up

<error message from widget-preview>
Could you fix this error by correcting the JSON file?

### Output

#### Fix 2 - Visualization + Errors

Failed to create widget - unexpected discriminator: string

- Upon follow-up question to fix JSON
  - Provided correct result! (See file)

#### Fix 1 - Field Types

Failed to create widget - Missing required field: reference_name

- No change

#### Original

Failed to create widget - Missing required field: reference_name
