# Velocity Discord

Chat from all servers gets bridged with a discord channel

## Features

- Configurable
- Webhooks or normal chat for messages
- Player count in bot status
- List command
- Templating syntax for all messages
- Death and Advancement messages shown

> **Note**
> This requires a [companion mod/plugin](https://github.com/unilock/YepTwo) for death/advancement messages

## Installation

1. Create a bot application [here](https://discordapp.com/developers/applications/)
   - Go to the `Bot` tab and click `Add bot`
2. Enable the `SERVER MEMBERS INTENT` and `MESSAGE CONTENT INTENT` under `Privileged Gateway Intents`
3. Copy the bot's token, you might have to click `Reset Token` first
4. Install the plugin on your server, start the server once, then stop the server again
5. Open the plugin config file at `plugins/discord/config.toml`
6. Under `[discord]`, paste your token in place of `TOKEN`
7. Under `[discord]`, paste the channel id you want to use
   - To get a channel id, you have to enable developer mode in Discord
   - Open Discord settings, go to `Advanced`, then turn on `Developer Mode`
   - Now right-click the channel you want to use and click `Copy ID`
8. Set any additional config options you want
9. Start the server and check if it works

## Configuration

Default config generated on startup:

```toml
# Don't change this
config_version = "1.8"

# Comma separated list of server names to exclude from the bridge (defined under [servers] inside your velocity.toml)
# e.g., exclude_servers = ["lobby", "survival"]
exclude_servers = []
excluded_servers_receive_messages = false

[discord]
# Bot token from https://discordapp.com/developers/applications/
token = "TOKEN"
# Channel ID to send Minecraft chat messages to
channel = "000000000000000000"

# Show messages from bots in Minecraft chat
show_bot_messages = false
# Show clickable links for attachments in Minecraft chat
show_attachments_ingame = true

# Show a text as playing activity of the bot
show_activity = true
# Activity text of the bot to show in Discord
# Placeholder {amount} is available
activity_text = "with {amount} players online"

# Enable mentioning Discord users from Minecraft chat
enable_mentions = true
# Enable @everyone and @here pings from Minecraft chat
enable_everyone_and_here = false

# OPTIONAL - Use a Discord webhook to have the bot use the player's username and avatar when sending messages
# Requires a webhook URL to be set below
use_webhook = false

[discord.webhook]
# Full webhook URL to send more fancy Minecraft chat messages to
webhook_url = ""
# Full URL of an avatar service to get the player's avatar from
# Placeholders {uuid} and {username} are available
avatar_url = "https://crafatar.com/avatars/{uuid}?overlay"
# The format of the webhook's username
# Placeholders {username} and {server} are available
webhook_username = "{username}"

# Minecraft > Discord message formats
# Uses the same formatting as the Discord client (a subset of markdown)
# Messages can be disabled with empty string ("") or false
[discord.chat]
# The format set in the following key "discord.chat.message" is ignored when a webhook is used
# Placeholders {username}, {server}, and {message} are available
# Can be disabled
message = "{username}: {message}"
# Placeholders {username} and {server} are available
# Can be disabled
join_message = "**{username} joined the game**"
leave_message = "**{username} left the game**"
# Possible different format for timeouts or other terminating connections
# Placeholder {username} is available
# Can be disabled
disconnect_message = "**{username} disconnected**"
# Placeholders {username}, {current}, and {previous} are available
# Can be disabled
server_switch_message = "**{username} moved to {current} from {previous}**"
# Placeholders {username} and {death_message} are available
# Can be disabled
death_message = "**{username} {death_message}**"
# Placeholders {username}, {advancement_title}, and {advancement_description} are available
# Can be disabled
advancement_message = "**{username} has made the advancement __{advancement_title}__**\n_{advancement_description}_"

[discord.commands.list]
enabled = true
# Ephemeral messages are only visible to the user who sent the command
ephemeral = true
# Placeholders {server_name}, {online_players} and {max_players} are available
server_format = "[{server_name} {online_players}/{max_players}]"
# Placeholder {username} is available
player_format = "- {username}"
# Can be disabled
no_players = "No players online"
# Can be disabled
server_offline = "Server offline"
codeblock_lang = "asciidoc"

# Discord > Minecraft message formats
# Uses XML-like formatting with https://docs.adventure.kyori.net/minimessage#format
[minecraft]
# Placeholder {discord} is available
discord_chunk = "<dark_gray>[<{discord_color}>Discord<dark_gray>]<reset>"
# Placeholders {role_color}, {username} and {nickname} are available
username_chunk = "<{role_color}><hover:show_text:{username}>{nickname}</hover><reset>"
# Placeholders {discord_chunk}, {username_chunk}, {attachments} and {message} are available
message = "{discord_chunk} {username_chunk}<dark_gray>: <reset>{message} {attachments}"
# Placeholders {url} and {attachment_color} are available
attachments = "<dark_gray><click:open_url:{url}>[<{attachment_color}>Attachment<dark_gray>]</click><reset>"
# Colors for the <{discord_color}> and <{attachment_color}> tags
discord_color = "#7289da"
attachment_color = "#4abdff"
```
