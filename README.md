---
description: Installing and configuring your code
---

# Installation & Setup

## Installing

{% tabs %}
{% tab title="NPM" %}
```shell
npm install @top-gg/voting-sdk
```
{% endtab %}

{% tab title="Yarn" %}
```shell
yarn add @top-gg/voting-sdk
```
{% endtab %}
{% endtabs %}

## Code

Once you've installed the library you can start adding code!

```javascript
const { VotingSDK } = require('@top-gg/voting-sdk');

// Setup the votingSDK for receiving webhooks
// Make sure to set your authorization to something unique!
const topgg = new VotingSDK("authorization", {
    port: 3000,
    path: "/topggwebhook"
});

// Initilize the databases and starts the webhook listener
await topgg.init();
```

## Configuring Top.gg

In order for Top.gg to know where to send webhooks you'll need to do some configuring. You can find the webhooks page on your bot/servers edit page, in the webhook section.\
[You can see your listed bots/servers here](https://top.gg/user/me).

<figure><img src="https://i.imgur.com/4Z4FWZT.png" alt=""><figcaption><p>Edit webhooks</p></figcaption></figure>

### The Authorization

The authorization is like a password. Top.gg will include it in all webhook requests, this library will check the authorization Top.gg sends to make sure its the same as the one you have in code. It can be anything you want, but it must be the same between Top.gg and your code!

### The webhook URL

The webhook URL will depend on your host, and the settings you use with the library.
You can find out more on the ["Finding your URL" guide](guides/finding-your-url.md).

{% hint style="warning" %}
The URL cannot be a Discord webhook URL, Topgg webhooks are not directly compatible with Discord webhooks!
{% endhint %}
