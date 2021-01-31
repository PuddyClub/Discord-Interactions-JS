<div align="center">
<p>
    <a href="https://discord.gg/TgHdvJd"><img src="https://img.shields.io/discord/413193536188579841?color=7289da&logo=discord&logoColor=white" alt="Discord server" /></a>
    <a href="https://www.npmjs.com/package/@tinypudding/discord-slash-commands"><img src="https://img.shields.io/npm/v/@tinypudding/discord-slash-commands.svg?maxAge=3600" alt="NPM version" /></a>
    <a href="https://www.npmjs.com/package/@tinypudding/discord-slash-commands"><img src="https://img.shields.io/npm/dt/@tinypudding/discord-slash-commands.svg?maxAge=3600" alt="NPM downloads" /></a>
    <a href="https://www.patreon.com/JasminDreasond"><img src="https://img.shields.io/badge/donate-patreon-F96854.svg" alt="Patreon" /></a>
</p>
<p>
    <a href="https://nodei.co/npm/@tinypudding/discord-slash-commands/"><img src="https://nodei.co/npm/@tinypudding/discord-slash-commands.png?downloads=true&stars=true" alt="npm installnfo" /></a>
</p>
</div>

# Discord-Interactions-JS
A simple way to interact and manage discord slash-commands.

# Credits
This module has been forked to be adapted to the scripts of the Tiny Pudding Server repositories.
The first version was made by https://github.com/MatteZ02/discord-interactions.

# Usage
You need to choose whether to type a Bot Token or a User Token.
```js
const interactions = require("@tinypudding/discord-slash-commands");

const client = new interactions.Client({
    bot_token: "you unique bot token",
    client_id: "your bots user id",
    user_token: "you unique user token"
});
```

## List all your existing commands.
```js
client.getCommands().then(console.log).catch(console.error);
```

## Will create a new command and log its data. If a command with this name already exist will that be overwritten.
```js
client
  .createCommand({
    name: "unique command name",
    description: "description for this unique command",
  })
  .then(console.log)
  .catch(console.error);
```

## Will edit the details of a command.
```js
client
  .editCommand(
    { name: "new command name", description: "new command description" },
    "id of the command you wish to edit"
  )
  .then(console.log)
  .catch(console.error);
```

## will delete a command
```js
client
  .deleteCommand("id of the command you wish to delete")
  .then(console.log)
  .catch(console.error);
```

# API

Passing a guildID is optional. Doing so will make the command only be available on that guild.
Guild commands update **instantly**. We recommend you use guild commands for quick testing, and global commands when they're ready for public use.

[Discord api documentation on slash commands](https://discord.com/developers/docs/interactions/slash-commands)

### getCommands(options: getCommandOptions) returns Promise< array of ApplicationOptions>

- `getCommandsOptions` - List of options can be found [here](#options).

### createCommand(options: ApplicationCommandOptions, guildID?: string) returns Promise<ApplicationOptions>

- `ApplicationOptions` - List of options can be found [here](#options).
- `guildID` - guild to create this command on.

### editCommand(options: ApplicationCommandOptions, commandID: string, guildID?: string) returns Promise<ApplicationOptions>

- `ApplicationOptions` - List of options can be found [here](#options).
- `commandID` - ID of the command you wish to edit.
- `guildID` - If the command is a part of a guild you must pass the guildID here.

### deleteCommand(commandID: string, guildID?: string)  returns Promise<boolean>

- `commandID` - ID of the command you wish to delete.
- `guildID` - If the command is a part of a guild you must pass the guildID here.

# Options

Properties marked with `?` are optional.

### ApplicationCommandOption

```js
{
    name: "name of this unique command",
    description: "description for this unique command",
    options?: [
        {
        name: "name of this option",
        description: "description for this option",
        type: 1,// Type for this option. for a list of types see https://discord.com/developers/docs/interactions/slash-commands#applicationcommandoptiontype
        default?: true,
        required?: true,
        choices?: [
            {
                name: "string to prefill for this choice",
                value: "value of this choice that will be returned when command is used."
            }
        ]
        }
    ]
}
```

```js
{
  name: "name of the command";
  description: "description of the command";
  options?: Array of ApplicationCommandOption;
}
```

### getCommandsOptions

```js
{
  commandID?: "id of the command you wish to get",
  guildID?: "if the command is a part of a guild u should put the guild id here"
}
```

### Types

You can find a list of Data Models and Types from [here](https://discord.com/developers/docs/interactions/slash-commands#data-models-and-types).

# Interaction with the command

You can setup a webhook-based interaction. You can read more about how to do this from the [documentation](https://discord.com/developers/docs/interactions/slash-commands#receiving-an-interaction).

### interaction example response

```JS
channel: Discord.TextChannel;// The channel where this interaction occured
guild: Discord.Guild;// The guild where this interaction occured
member: Discord.GuildMember | null;// The guild member who issued the interaction (will be null if we cannot obtain a guildMember)
author: Discord.User | null;// The user who issued the interaction (will be null if we cannot obtain an user)
name: string;// name of this command
content: string;// content of this command (everything after the main command name)
createdTimestamp: number;// timestamp of this command being used
options: { value: string; name: string }[] | null;// list of options this user inputted to the command
```