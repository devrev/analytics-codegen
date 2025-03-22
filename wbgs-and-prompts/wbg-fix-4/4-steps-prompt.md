# Steps for model prompt

Plese refer to `model-prompt.md` for the prompts.
NOTE: The angle brackets <> tell you what to do for each prompt.
Specifically, follow these steps with the LLM:

- Find the base query and table schema
  - If testing on your own data, open DevRev Notebook UI
    - Find and download each data table
      - Look for tables in the search box
      - Click on the download button next to each table
        - Should turn into a checkmark once downloaded, wait a couple seconds
    - Generate an SQL query and ensure it runs
      - Copy the query for later use
    - Find the table schemas for each table
      - Look for the diagonal arrow next to each table in the search box
        - A pop-up window appears with the table schema
        - Copy this for later use
  - If you would like to use a pre-existing widget - Obtain the widget ID from a dashboard - Dashboards can be found under Explore > checkmark Dashboards - Go to Dashboard Preview UI: `app.devrev.ai/devrev/dashboard-preview` - Go into Chrome Developer Tools > Network > search for 'dashboard' > obtain its ID - Alternatively, look for the ID in the URL, after `dashboardId` - i.e. dashboard URL = `https://app.devrev.ai/devrev/dashboard?dashboardId=don%3Adata%3Advrv-us-1%3Adashboa[…]ays%22%2C%22presetValue%22%3A30%2C%22type%22%3A%22preset%22%7D` - Here, `dashboardId=don%3Adata%3Advrv-us-1%3Adashboard%2FjoDZWGmRDo` - NOTE: This ends right before `&dashboardToken` - Within the ID, replace: - `%3A` with `:` - `%2F` with `/` - Find the widget ID within the dashboard JSON file - Paste the widget ID into Widget Preview UI
    - If you want to test a widget from one of the files in this repo
      - Go to the dataset name, `trials` file:
        - i.e. `\wgt-gen\article-analytics-total-vieww\trials-article-analytics-total-views.md`
        - Copy the base query, after the line `This is the base query:`
        - Copy the entire table schema, from after the line `Here is the table schema`
          - Ensure you copy all of it, starting with each table name until you reach the end of the schema
- Open `model-prompt.md`
- Create a new chat with the LLM of your choice
- For each prompt #, i.e. `## Prompt 1` and `## Prompt 2`, etc., follow the steps below:
  - Paste the entire prompt into the chat
    - For the very first prompt:
      - Replace <Provide table schema> with the table schema obtained above
      - Replace <Provide base query> with the base query obtained above
    - For all prompts, regardless of #:
      - Replace the <Attach <file-name>.md> line with the content of that <file-name>
        - i.e. if it says <Attach \*-widget-building-guide.md>
        - Copy the contents of `3-widget-building-guide.md` (or whichever # it starts off with)
          - Pick the highest-numbered file, as this is the most-recent version
- Run query to obtain the corresponding JSON template
- Copy the contents of the generated JSON in Widget Preview UI and click on `Create Widget`
  - If there is an error, paste the corresponding `### Follow-Up Prompt` into the chat
    - Replace the content of the file with the <Attach <file-name>.md> line, as done previously
      - i.e. if it says <Attach \*-widget-building-guide.md>
    - Replace <Attach \*errors-to-fix.md> with the most recently-numbered file, i.e. `3-errors-to-fix.md` content
- Run this to ese if the model can fix the JSON according to the error from the UI
  - If not, try again
  - Otherwise, move onto the next prompt
- At `## Prompt 5` the model should have generated a JSON
  - Test this against the UI to catch any errors
