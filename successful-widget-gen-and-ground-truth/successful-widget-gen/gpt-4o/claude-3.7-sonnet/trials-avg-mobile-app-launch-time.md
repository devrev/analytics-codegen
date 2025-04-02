# Input

Given the base SQL query:
SELECT network_operator, AVG(app_launch_time) AS avg_launch_time FROM system.mobile_sessions_metadatas_v1 GROUP BY network_operator ORDER BY avg_launch_time

And the table schema:
mobile_sessions_metadatas_v1Schema session_id VARCHAR created_at TIMESTAMP version_key VARCHAR identifier VARCHAR network_operator VARCHAR network_type VARCHAR first_user_interaction BIGINT app_launch_time BIGINT app_launch_type VARCHAR device_manufacturer VARCHAR device_name VARCHAR app_version VARCHAR exception_type VARCHAR error_count BIGINT is_rage BIGINT ux_evaluation VARCHAR platform VARCHAR

Understand the widget building guide below fully for how to create a widget. Keep in mind the base query and table schema. Generate the JSON configuration for a widget of average app launch time in a bar graph.

# Follow-Up

 <paste error here>

# Trials

## Fix 6 - Instructions + Code

Success: Binder Error solved quicker, precision error solved again in one shot

don:data:dvrv-us-1:devo/0:widget/6P9LHCAM7U

- Table w/o NULL values - successful!

don:data:dvrv-us-1:devo/0:widget/GgFUkaAAtK

- Bar chart - all values - successful!

don:data:dvrv-us-1:devo/0:widget/aINjCe65uf

- Stacked-bar graph: Avg. vs Max. launch time - successful!

WRONG WIDGETS:

- First couple do not display, like last time

CONVO:

Error: Binder Error: Referenced column "app_launch_time" not found in FROM clause! Candidate bindings: "mobile_sessions_data.avg_launch_time" LINE 1: SELECT AVG(app_launch_time) AS mobile_sessions_dat... ^

- Fixed in one shot!
  - Unlike last time, which took 3x
  - This means added instructions worked!

Failed to create widget - Invalid field: precision

- Fixes error - just like last time!

Widget created successfully! But it deos nto display. What can be done?

- Suggests options: null handling, permission issues
  - Applies these fixes to file
  - None of which work

Widget created successfully, but it still does not display

- Switches to table visualization
  - Simplifies query - query issue
  - Adds NULL handling

Could you make this into a bar graph? And line chart?

- Successfully creates both graphs
  - Understands that we need two separate widgets
  - Creates two different, working JSONs, as expected (see above IDs)

Now, could you make a stacked bar graph with avg. vs total launch times?

- Successfully produces stacked bar graph
  - Realizes that total time is not a good metric
  - Suggests maximum launch time, instead
  - Creates widget that works! (Imporvement from last time:)

## Fix 5 - Cheat Sheet

don:data:dvrv-us-1:devo/0:widget/QhczBI3Cmf

- Donut chart - top 5 values - successful!

don:data:dvrv-us-1:devo/0:widget/LNqYcscHP7

- Table representation w/ top 5 values - successful!

don:data:dvrv-us-1:devo/0:widget/Rgzd2EV4C1

- Table representation w/o NULL values - successful!

WRONG IDs:
don:data:dvrv-us-1:devo/0:widget/fUJkeFSsqm
don:data:dvrv-us-1:devo/0:widget/rtrsJxHC82

- Column chart representaiton that does not display
- Initially created widget, but no graph

CONVO:
Error: Binder Error: Referenced column "app_launch_time" not found in FROM clause! Candidate bindings: "mobile_sessions_metadatas_v1.average_app_launch_time" LINE 1: SELECT AVG(app_launch_time) AS mobile_sessions_met... ^

- This error was seen thrice
  - Fixed 3rd time

Failed to create widget - Invalid field: precision

It created a widget, but i cannot see the graph. Is this because precision field was removed?

- Gave two outputs:
  - Changed visualization to column (vertical) bar graph
    - Created widget w/o display
  - Changed visualization to table, removing any possible NULL values by modifying query
    - Worked after NULL values removed

The table visualization worked! Cuold you convert this to a column chart?

- Appaeared, but could not create widget

The column chart does not display. Could you convert it to another visualization that is not a table, but appropriately displays?

- Produced a line and donut chart JSON config
  - Both appeared momentarily on screen, but again did not display when widget was created

None of these charts are displaying. Once you click on the metrics to find out what they are, the graph suddenly disappears. What might be the problem?

- Produced a line and donut chart
- Both did not display

None of these charts are displaying. Once you click on the metrics to find out what they are, the graph suddenly disappears. What might be the problem?

- Produced a matric chart that worked (NOTE: ID not saved above)
- Created a table of top 5 values that had an error:

For the top five table:
Expected double-quoted property name in JSON at position 1665 (line 50 column 21)

- Fixed error, successful widget creation!

It created successfully, could you convert this into a donut chart?

- Successful donut widget created!
