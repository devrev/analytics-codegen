# Prompt for LLM

## Prompt 1: Widget Building Guide

You are going to be an expert at generating a widget, given the following information.

First, this is the base SQL query you need to know:
<Porvide base query>

Then, there's the table schema:
<Provide schema of each table, with table name, followed by new line>

Understand the widget building guide attached fully for how to build a widget. Keep in mmind the base query and table(s) schema for widget creation.

<Attach \*-wbg.md>

## Prompt 2: Data Source

Considering what you have already learned from the widget building guide, here is a guide for creating the data source section of the JSON file for the widget. Carefully read through it and produce the data source part of the widget.

<Attach \*-data-source.md>

## Follow-Up 2: Data Source

There was an error with the data source section you put together previously.

<Paste error here>

Plese once again understand the attached file on how to generate a correct data source.
Also, learn how to fix common errors with the errors' file attached.

Could you fix the data source JSON code?

<Attach \*-data-source.md>
<Attach \*-errors-to-fix.md>

## Prompt 3: Base Query

Take a look at the base query you have inserted within the data source. Does it allude to the rules within the attached guide ofr base queries? If not, fix it according to what you understand from this file.

<Attach \*-base-query.md>

## Follow-Up 3: Base Query

There was an error with the base query you put itno the data source.

<Paste error here>

Plese once again understand the attached file on how to generate a correct base query.
Also, learn how to fix common errors with the errors' file attached.

Could you fix the base query within the data source?

<Attach \*-base-query.md>
<Attach \*-errors-to-fix.md>

## Prompt 4: Sub-Widgets

Now, I would like you to create the sub-widget section of the JSON file by fully grasping the content of the attached file on hwo to do that.

<Attach \*-sub-widget.md>

## Follow-Up 4: Sub-Widgets

There was an error with the sub-widget section you created.

<Paste error here>

Plese once again understand the attached file on how to generate a correct sub-widget section.
Also, learn how to fix common errors with the errors' file attached.

Can you fix this section accordingly?

<Attach \*-sub-widget.md>
<Attach \*-errors-to-fix.md>

## Prompt 5: Widget JSON File

Putting all of these secions together, and from what you have learned through this process, generate teh entire JSON file for the widget. Ensure it follows the widget building guide, attached once again for your convenience. Make sure it creates a widget with the proper format, structure, and xyntax.

<Attach \*-wbg.md>

## Follow-Up 5: Widget JSON File

We've encountered an error when processing the widget file.

<Paste error here>

Plese once again understand the attached file on how to generate a correct JSON file for a widget.
Also, learn how to fix common errors with the errors' file attached.

Can you fix the JSON file, so that it creates a working widget?

<Attach \*-wbg.md>
<Attach \*-errors-to-fix.md>
