# Example code

{% code title="Index.js" %}
```javascript
const { Client, Events, GatewayIntentBits, ActionRowBuilder, ButtonBuilder, ButtonStyle } = require('discord.js');
const { token } = require('./config.json');
const client = new Client({ intents: [GatewayIntentBits.Guilds, GatewayIntentBits.GuildMessages] });


const { VotingSDK } = require('@top-gg/voting-sdk');
const topgg = new VotingSDK(process.env.webhookAuth, { // create a new votingSDK instance
  testReminderTime: 5,
  port: 3000,
  remindersOptInDefault: true,
})

topgg.on('vote', async vote => { // runs when topgg receives a vote
  const user = await client.users.fetch(vote.user);
  await user.send({
    embeds: [
      {
        title: "You voted for Luca!",
        url: `https://top.gg/bot/${client.user.id}/vote`,
        thumbnail: {
          url: client.user.avatarURL()
        },
        description: `You can vote for <@${client.user.id}> in <t:${Math.round(new Date().setHours(new Date().getHours() + 12) / 1000)}:R>.\nYou have vote reminders __${await topgg.getOpt(vote.user) ? 'Enabled' : 'Disabled'}__`,
        color: "16724582",
      }
    ],
    components: [
      new ActionRowBuilder()
        .addComponents(
          new ButtonBuilder()
            .setCustomId('enablereminders')
            .setLabel("Enable remidners")
            .setStyle(ButtonStyle.Primary)
            .setDisabled(await topgg.getOpt(vote.user)),
          new ButtonBuilder()
            .setLabel("Open Vote Page")
            .setStyle(ButtonStyle.Link)
            .setURL(`https://top.gg/bot/${client.user.id}/vote`),
        )
    ]
  })
})
topgg.on('reminder', async reminder => { // runs if someone has reminders enabled, or they are currently enabled & the user didnt disbale them.
  const user = await client.users.fetch(reminder.id);
  await user.send({
    embeds: [
      {
        title: "You can vote for Luca again!",
        url: `https://top.gg/bot/${client.user.id}/vote`,
        thumbnail: {
          url: client.user.avatarURL()
        },
        description: `You can vote for <@${client.user.id}> every **12 hours**. Keep voting!`,
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

topgg.on('testVote', vote => { // log the test event to make sure it works!
  console.log("testVote")
  console.log(vote)
})
topgg.on('testReminder', reminder => { // log the test remidner event to make sure it works!
  console.log("testReminder")
  console.log(reminder)
})


client.once(Events.ClientReady, async c => {
  console.log(`Ready! Logged in as ${c.user.tag}`);
});

client.on(Events.InteractionCreate, async interaction => { // listen for the disablereminders and enable reminders buttons
  if (!interaction.isButton()) return;
  if (interaction.customId === "disablereminders") {
    await topgg.optOut(interaction.user.id); // disable reminders
    return interaction.reply("Reminders have been disabled!")
  }
  if (interaction.customId === "enablereminders") {
    await topgg.optIn(interaction.user.id); // enable reminders
    return interaction.reply("Reminders have been enabled!")
  }
})

topgg.init(); // initilize the topgg library
client.login(token);
```
{% endcode %}
