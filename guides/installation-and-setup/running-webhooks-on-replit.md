---
description: Replit doesnt provide a public IP, it will provide you with a url!
---

# Running webhooks on Replit

When you run your project with the library Replit will open a "Webview". At the top of the webview Replit will show your base URL.

<figure><img src="https://i.imgur.com/EBxyrG0.png" alt=""><figcaption><p>Finding your replit base URL</p></figcaption></figure>

In this example my base url is `https://Voting-SFK.woowoo4.repl.co`

In the code you can see the path is set to `/topggwebhook`.\
So my full URL is: `https://Voting-SFK.woowoo4.repl.co/topggwebhook`

## Secrets or Enviorment variables

Replit is not private, all code on the free tier is publically viewable. If you place your webhook authentication directly in your code anyone can see it!

```javascript
const topgg = new VotingSDK("SomeSuperSecretAuth!", {
  port: 3000,
  path: "/topggwebhook"
})
```

Instead you'll want to use Replit secrets.

<figure><img src="https://i.imgur.com/opYsfQY.png" alt=""><figcaption><p>Secrets can be found in tools</p></figcaption></figure>

<figure><img src="https://i.imgur.com/FsOblFP.png" alt=""><figcaption><p>Adding a webhookAuth secret</p></figcaption></figure>

Once you add your secret you can change your code to

```javascript
const topgg = new VotingSDK(process.env['webhookAuth'], {
  port: 3000,
  path: "/topggwebhook"
})
```

## Using the Voting SDK with uptime services.

There is a good chance you use an uptime service to keep your Replit instance running. You'll problably need to change some code otherwise Replit might give some errors.

I'd suggest removing the old code for your uptime service and instead adding something like this.

```javascript
// Create a webpage for any uptime service.
topgg.app.get('/', (req, res) => res.send('hi!'))
```
