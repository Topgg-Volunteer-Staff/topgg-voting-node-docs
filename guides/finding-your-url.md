---
description: Your webhook url is where Top.gg sends vote information to.
---

# Finding your URL

This page is for hosts with public IP's, or hosting from home.\
If you're using Replit go to the [Replit Page](installation-and-setup/running-webhooks-on-replit.md)

## URL structure

When using webhooks a domain is not necessary, instead you can use your IP.\
The structure is simple. `http://YOURIP:PORT/PATH`

## Finding your public IP

Most hosts will provide you a public IP, you can find this public IP in the dashboard of your host. If you're unsure where to find it contact your hosts support.\
\
For developers hosting from home refer to [this](installation-and-setup/running-webhooks-from-home.md#finding-your-public-ip).

{% hint style="warning" %}
Make sure not to use a private IP, or an internal IP. Webhooks need to reach your code using public means, private IP's are used internally.
{% endhint %}

{% hint style="danger" %}
IP's are sensitive information, you should not be sharing it with other users.
{% endhint %}

## Your port and path

The post and path is something you set in code.

```javascript
const topgg = new VotingSDK("SomeSuperSecretAuth!", {
  port: 3000,
  path: "/topggwebhook",
});
```

By default the VotingSDK will set the port to 3000 and the path to "/topggwebhook".\
So your URL would look something like this. `http://YOURIP:3000/topggwebhook`.
