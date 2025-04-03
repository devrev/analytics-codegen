# Add to Prompt

## Prompt: Fix 7

1. Add only required dimensions/measures
2. Filter out columns that are unnecessary in query

DONE:

1. Test edge-case

   - Fix user-specified SQL query before proceding
     - Look at Binder Errors and suggest ideas

2. Ensure widget config does not include added fields

3. If "Widget Created Successfully!", but does not display
   - Ask before changing visualization type or what data the widget displays

ADD to CLI:

1. If "Widget Created Successfully!", but does not display

   - Ask before changing visualization type or what data the widget displays

2. User permission to access data

   - Admin permission

3. Ensure user provides two things, outside of base query/schema:
   - Widget description - what it displays
     - This has to be specific, i.e. "performance incident count" instead of "incident count"
   - Widget title - IF desired!
   - Visualization type
