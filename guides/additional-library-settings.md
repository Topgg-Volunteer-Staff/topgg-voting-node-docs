# Additional library settings

{% code title="Example" %}
```javascript
const topgg = new VotingSDK("SomeSuperSecretAuth!", {
  path: "/topggwebhook",
  port: 3000,
  dbPath: "./voters.db",
  reminderTime: 43200,
  interval: 10,
  testDbPath: ":memory:",
  testReminderTime: 43200,
  remindersOptInDefault: false
})
```
{% endcode %}

{% code title="path" %}
```javascript
// The path is a string that goes at the end of your URL.
// It must start with /
{ path: "/topggwebhook" }
```
{% endcode %}

{% code title="port" %}
```javascript
// The port is used to set what port the webhook will listen on
// It must be a number
{ port: 3000 }
```
{% endcode %}

{% code title="dbPath" %}
```javascript
// dbPath is used to set the location to save the database
// It must start with ./
{ dbPath: "./voters.db" }
```
{% endcode %}

{% code title="reminderTime" %}
```javascript
// reminderTime sets the number of seconds to wait to send reminders
// It must be a number
{ reminderTime: 43200 }
```
{% endcode %}

{% code title="interval" %}
```javascript
// interval sets the number of seconds to wait between checking for expired votes
// It must be a number
{ interval: 10 }
```
{% endcode %}

{% code title="testDbPath" %}
```javascript
// testDbPath is used to set the database path for test votes/reminders
// By default its set to :memory: which stores test votes in memory.
{ testDbPath: ":memory:" }
```
{% endcode %}

{% code title="testReminderTime" %}
```javascript
// reminderTime sets the number of seconds to wait to send reminders for test votes
// It must be a number
{ testReminderTime: 43200 }
```
{% endcode %}

{% code title="remindersOptInDefault" %}
```javascript
// remindersOptInDefault sets if reminders should be enabled for voters by default
// It must be true or false
{ remindersOptInDefault: false }
```
{% endcode %}
