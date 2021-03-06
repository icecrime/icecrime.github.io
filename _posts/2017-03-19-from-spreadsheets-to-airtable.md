---
layout: post
title: "From spreadsheets to Airtable"
description: "An introduction to using Airtable."
tags: [organization, tooling]
categories: [Technology]
---

I work in a fast paced startup as the manager for a dozen (amazing) engineers who typically deal with 2 to 5 simultaneous tasks at any given time. As a result, one aspect of my job is to keep track of all of those items and know:

- What we're doing, and what's the current status.
- Who is involved on each, and whether the load is appropriately distributed.
- Whether the team needs help to make progress.

I'll use this specific example to describe how I moved away from spreadsheets in favor of [Airtable](https://www.airtable.com) and what it buys me.

# Your typical spreadsheet

Here's a simplified and anonymized version of the spreadsheet I had been using so far:

<figure class="center">
    <a href="/images/airtable/spreadsheet_1.png"><img src="/images/airtable/spreadsheet_1_crop.png" alt=""></a>
    <figcaption><a href="/images/airtable/spreadsheet_1.png" title="Task management spreadsheet">Task management spreadsheet</a>.</figcaption>
</figure>


All the information is there, _but_:

- Getting from zero to a spreadsheet like this one takes _some_ time. You need to structure as a table, set up data validation, set up conditional formatting.
- Maintenance is painful: for example adding a category requires updating the scaffolding accordingly.
- Data cannot easily be queried: filtering allows to narrow down to a subset of categories or statuses, but that's basically it.

In other words, there's some overhead and hygiene involved in making a spreadsheet behave like a database.

# Introducing Airtable

I would describe [Airtable](https://www.airtable.com) as **a relational database wrapped under a familiar and accessible spreadsheet UI**. Where spreadsheets enforce no particular structure, every sheet in Airtable is really a **table** storing **records** under a well-defined **schema** . By design, implementing the example spreadsheet above in Airtable takes no more than a minute because the only effort resides in the schema definition: once done the UI is _meant_ to manage records according to that schema.

We'll start with Airtable's ability to import existing data (either through CSV or copy/pasting fields), go through each column to update its data type (hence defining our schema), and _tada_:

<figure class="center">
    <a href="/images/airtable/tasks_airtable_1.png"><img src="/images/airtable/tasks_airtable_1_crop.png" alt=""></a>
    <figcaption><a href="/images/airtable/tasks_airtable_1.png" title="Migrating to Airtable">Migrating to Airtable</a>.</figcaption>
</figure>

At this point it may seem like we traded one UI for another, but there are already concrete benefits:

- We get a nice form UI for adding and managing records.
- The table structure and schema are enforced.
- Maintenance is trivial: for example, I can add a category in a second. 

But it's gets much better.

## Leveraging views

Airtable has a straightforward UI for grouping and sorting: pretty much Pivot Tables for humans. For example, we can trivially group tasks by category, and sort by ascending update date.

<figure class="center">
    <a href="/images/airtable/tasks_airtable_2.png"><img src="/images/airtable/tasks_airtable_2_crop.png" alt=""></a>
    <figcaption><a href="/images/airtable/tasks_airtable_2.png" title="Grouping by category">Grouping by category</a>.</figcaption>
</figure>

From there you can persist the settings as separate [views](https://support.airtable.com/hc/en-us/articles/202624989-Guide-to-views) and even create non-grid views, such as a [Kanban board](https://support.airtable.com/hc/en-us/articles/229848887-Guide-to-kanban-view).

<figure class="center">
    <a href="/images/airtable/tasks_airtable_3.png"><img src="/images/airtable/tasks_airtable_3_crop.png" alt=""></a>
    <figcaption><a href="/images/airtable/tasks_airtable_3.png" title="The Kaban view">The Kaban view</a>.</figcaption>
</figure>

## Leveraging relations

Let's see how the "relational" dimension of Airtable can help us improve further. So far the "Who" column is just free text: we can create a "Team" table with the team members, and convert the "Who" colum to a [Linked Record](https://support.airtable.com/hc/en-us/articles/206452848-Linked-record-fields).

<figure class="center">
    <a href="/images/airtable/tasks_airtable_4.png"><img src="/images/airtable/tasks_airtable_4_crop.png" alt=""></a>
    <figcaption><a href="/images/airtable/tasks_airtable_4.png" title="Leveraging relations">Leveraging relations</a>.</figcaption>
</figure>

The "Who" column being a linked record gives you everything you would expect from a relational database. Airtable's UI is again really key here, as it's trivial to select a record from the People table from the Tasks table, and even create new People entries as a task is being added.

More importantly, Airtable automatically created the other side of the relationship in the People table: we basically get the list of task assigned to each individual team member for free.

<figure class="center">
    <a href="/images/airtable/tasks_airtable_5.png"><img src="/images/airtable/tasks_airtable_5_crop.png" alt=""></a>
    <figcaption><a href="/images/airtable/tasks_airtable_5.png" title="The other side of the relation">The other side of the relation</a>.</figcaption>
</figure>

# Summing up

Spreadsheets are great, but for anything that ressembles a database with structured records the boilerplate for the initial setup and maintenance cannot be ignored. This is one aspect where Airtable really shines: by providing a familiar spreadsheet-like UI to what is really a relational database under the hood, it eliminates a lot of the overhead while providing some immensely valuable benefits.

In this post we only scratched the surface: a thousands more things can be achieved when you start digging in [Airtable's API](https://airtable.com/api). More advanced use cases have been described by [Simon Eskildsen](https://twitter.com/sirupsen) on [his blog](http://sirupsen.com/airtable/).