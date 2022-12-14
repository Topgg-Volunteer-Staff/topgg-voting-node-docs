# Receiving Votes

<figure><img src="https://i.imgur.com/3QKgFcA.png" alt=""><figcaption></figcaption></figure>

Once you've configured Topgg and add the library to your code you can start receiving test votes and votes!\
\
Its often easier to start with test votes.

{% hint style="info" %}
You can find the test vote button the the edit page of your bot or server.
{% endhint %}

{% code title="Adding the test event" %}
```javascript
// This code will log a new test vote in console, with the vote data.
topgg.on("testVote", (vote) => {
    console.log(`test vote event: ${JSON.stringify(vote)}`)
})
```
{% endcode %}

### Once you've made sure you can receive test votes you can move on to real votes!

You can use this event to send the user a message on vote with discordJS(or any library!)\
You can also give rewards here.

{% tabs %}
{% tab title="DiscordJS" %}
```javascript
const { Client, GatewayIntentBits } = require('discord.js');
const { VotingSDK } = require('@top-gg/voting-sdk');

const client = new Client({ intents: [GatewayIntentBits.Guilds] });
client.login("token");


const topgg = new VotingSDK("authorization");

topgg.on("vote", async (vote) => {
    console.log(vote)
    const user = await client.users.fetch(user);
    user.send("We received your vote!")
})

topgg.init();
```
{% endtab %}
{% endtabs %}
