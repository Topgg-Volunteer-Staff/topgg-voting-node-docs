---
description: Databases store information for long periods of time.
---

# What is a database?

This library creates a database when you first use it.\
Databases are used by developers to store information for as long as its nessecary.\
\
Databases are made up of tables, those tables hold the actual information. This library will create two tables in the database.

## Table schema

### Voters

The voters table holds vote information. It contains two columns.\
The voters ID, and the time the vote occurred at.

{% tabs %}
{% tab title="Schema" %}
When a user votes their Discord ID and the current time is saved.\
The library will then periodically check this table for any votedAt timestamps that occured 12 hours ago or more. If a vote is expired it will be deleted from your database.

| Column  | Description                     |
| ------- | ------------------------------- |
| id      | The voters Discord Id           |
| votedAt | The timestamp the user voted at |
{% endtab %}

{% tab title="Example" %}
| ID                   | votedAt       |
| -------------------- | ------------- |
| "311553339261321216" | 1669738439228 |
| "136583532972605440" | 1669755535947 |
| "264811613708746752" | 1669732335351 |
{% endtab %}
{% endtabs %}

### voterOptions

The voterOptions table holds any options a user sets. The only setting is currently opting in or out of vote reminders.

{% tabs %}
{% tab title="Schema" %}
Before the reminder event is fired this database is checked, if a user is opted in to reminders OR the reminders are enabled by default the reminder event is fired. Otherwise it will not fire for that user.

| Column | Description                         |
| ------ | ----------------------------------- |
| id     | The voters Discord ID               |
| optIn  | If the voter wants voting reminders |
{% endtab %}

{% tab title="Example" %}
| ID                   | optIn |
| -------------------- | ----- |
| "311553339261321216" | false |
| "264811613708746752" | true  |
{% endtab %}
{% endtabs %}
