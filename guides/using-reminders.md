---
description: Enabling reminders & following Top.gg guidelines
---

# Using reminders

<figure><img src="https://i.imgur.com/mT2HHLw.png" alt=""><figcaption></figcaption></figure>

{% hint style="danger" %}
Top.gg has some guidelines for [voting reminders](https://support.top.gg/support/solutions/articles/73000502502-bot-guidelines). It's important to make sure you follow them. If you are sending reminder notifications you **MUST** include how to **opt out** of voting reminders in the message.
{% endhint %}

## Enabling reminders

By default new voters are not opted into reminders. You can find more about [changing options here](broken-reference).

## The reminder event

The reminder event fires 12 hours after someone votes, but only if they are enabled for all new voters, or if the user has manually opted into them.

```javascript
topgg.on("reminder", async (reminder) => { // reminder is { id: userID, votedAt: timestamp }
  const user = await client.users.fetch(reminder.id);
  await user.send({
    content: "You can vote for our bot again!",
    components: [
      new ActionRowBuilder()
        .addComponents(
          new ButtonBuilder()// add a button to let the user disable reminders.
            .setCustomId('disablereminders')
            .setLabel("Disable reminders")
            .setStyle(ButtonStyle.Primary),
          new ButtonBuilder() // add a button to open the vote page
            .setLabel("Open Vote Page")
            .setStyle(ButtonStyle.Link)
            .setURL(`https://top.gg/bot/${client.user.id}/vote`),
        )
    ]
  })
})java
```

{% hint style="warning" %}
Errors that occur inside this event will stop the vote from being removed, this means in the next few seconds the library will refire the event.\
If you don't want this to happen make sure to catch all potential errors!
{% endhint %}

## Handling enable/disable reminder buttons

The below code will watch for button presses with the custom IDs "disablereminders" & "enablereminders". If a user interacts with either it will disable/enable reminders for the user.

```javascript
client.on(Events.InteractionCreate, async (interaction) => {
  if (!interaction.isButton()) return;
  if (interaction.customId === "disablereminders") {
    await topgg.optOut(interaction.user.id);
    interaction.reply("Reminders have been disabled!");
  } else if (interaction.customId === "enablereminders") {
    await topgg.optIn(interaction.user.id);
    interaction.reply("Reminders have been enabled!");
  }
});
```
