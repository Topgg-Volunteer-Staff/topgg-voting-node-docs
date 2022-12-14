---
description: Understanding webhooks can be hard. Lets figure them out!
---

# What are Webhooks?

Webhooks are a way for one server to communicate with another server using http.

## What is HTTP? How does it work?

HTTP is used to send requests to other servers or services on the internet. Every site you visit uses HTTP for you to get or send information.\
\
HTTP is primarily two things, **requests** and **responses**. \
The request is a way for the client to get information or provide information.\
The response is the way the server responds, either containing the data requested, or a response to the new information(or an error message!).

## How do Top.gg's webhooks work?

When your bot or Discord server receives a vote we will send a HTTP request to the URL you have on the edit page of your bot or server.

{% hint style="warning" %}
The URL cannot be a Discord webhook URL, Top.gg webhooks are not directly compatible with Discord webhooks!
{% endhint %}

You can find out more about [finding your URL here](../guides/finding-your-url.md).

In the request Top.gg sends to you it will include several things.\
The most important is the authorization header. The authorization header can be thought of like a password between Top.gg and your webhook. The only time your webhook will accept a request is if the password is correct. You'll be the one deciding the authorization so make sure its secure, and don't share it with anyone!

## Other information Top.gg will send

| Field        | Type      | Description                                                                                         |
| ------------ | --------- | --------------------------------------------------------------------------------------------------- |
| bot or guild | snowflake | Discord ID of the bot or server that received a vote.                                               |
| user         | snowflake | Discord ID of the user who voted.                                                                   |
| type         | string    | The type of the vote (should always be `"upvote"` except when using the test button it's `"test"`). |
| isWeekend    | boolean   | Whether the weekend multiplier is in effect, meaning users votes count as two.                      |
| query?       | string    | Query string params found on the /bot/:ID/vote page. Example: ?a=1\&b=2.                            |
