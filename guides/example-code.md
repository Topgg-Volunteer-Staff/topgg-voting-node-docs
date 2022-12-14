---
description: This is an early example, I need to clean things up & add comments.
layout: editorial
---

# Example code

{% code title="Index.js" %}
```javascript
// Require the necessary discord.js classes
const { Client, Events, GatewayIntentBits, ActionRowBuilder, ButtonBuilder, ButtonStyle } = require('discord.js');
const { token } = require('./config.json');

const client = new Client({ intents: [GatewayIntentBits.Guilds, GatewayIntentBits.GuildMessages] });

const { VotingSDK } = require('@top-gg/voting-sdk');


const topgg = new VotingSDK(process.env.webhookAuth, {
  testReminderTime: 5,
  interval: 5,
  port: 3000,
  remindersOptInDefault: true,
})

topgg.on('vote', async vote => {
  console.log("vote")
  console.log(vote)
  const user = await client.users.fetch(vote.user);
  await user.send({
    embeds: [
      {
        title: "You voted for Luca!",
        url: "https://top.gg/bot/luca/vote",
        thumbnail: {
          url: "https://images.discordapp.net/avatars/264811613708746752/23c99475a6d570adc80223139a38fd4c.png"
        },
        description: `You can vote for <@264811613708746752> in <t:1670553780:R>.\nYou have vote reminders __${await topgg.getOpt(vote.user) ? 'Enabled' : 'Disabled'}__`,
        color: "16724582",
      }
    ],
    components: [
      new ActionRowBuilder()
        .addComponents(
          new ButtonBuilder()
            .setCustomId('enablereminders')
            .setLabel("Enable remidners")
            .setStyle(ButtonStyle.Primary),
          new ButtonBuilder()
            .setLabel("Open Vote Page")
            .setStyle(ButtonStyle.Link)
            .setURL("https://top.gg/bot/luca/vote"),
        )
    ]
  })
})
topgg.on('reminder', async reminder => {
  console.log("reminder")
  console.log(reminder)
  const user = await client.users.fetch(reminder.id);
  await user.send({
    embeds: [
      {
        title: "You can vote for Luca again!",
        url: "https://top.gg/bot/luca/vote",
        thumbnail: {
          url: "https://images.discordapp.net/avatars/264811613708746752/23c99475a6d570adc80223139a38fd4c.png"
        },
        description: "You can vote for <@264811613708746752> every **12 hours**. Keep voting!",
        color: "16724582"
      }
    ],
    components: [
      new ActionRowBuilder()
        .addComponents(
          new ButtonBuilder()
            .setCustomId('disablereminders')
            .setLabel("Disable reminders")
            .setStyle(ButtonStyle.Primary),
          new ButtonBuilder()
            .setLabel("Open Vote Page")
            .setStyle(ButtonStyle.Link)
            .setURL("https://top.gg/bot/luca/vote"),
        )
    ]
  })
})

topgg.on('testVote', vote => {
  console.log("testVote")
  console.log(vote)
})
topgg.on('testReminder', reminder => {
  console.log("testReminder")
  console.log(reminder)
})


client.once(Events.ClientReady, async c => {
  console.log(`Ready! Logged in as ${c.user.tag}`);
  console.log(await topgg.hasVoted('id', true))
});

client.on(Events.InteractionCreate, async interaction => {
  if (!interaction.isButton()) return;
  if (interaction.customId === "disablereminders") {
    await topgg.optOut(interaction.user.id);
    interaction.reply("Reminders have been disabled!")
  } else if (interaction.customId === "enablereminders") {
    await topgg.optIn(interaction.user.id);
    interaction.reply("Reminders have been enabled!")
  }
})

topgg.init()
// Log in to Discord with your client's token
client.login(token);

```
{% endcode %}
