# ServerProtect

A lightweight **Velocity proxy protection plugin** for blocking usernames before they can connect to your network.

## Features

* 🚫 Block players by username
* 🔒 Blocks players **before login**
* 🔤 Case-insensitive username matching
* 🎨 MiniMessage support
* ⚙️ Configurable kick message
* 🔄 Reload configuration without restarting Velocity
* 📝 Automatic `blocked.txt` management
* 💻 Console-only management commands
* 📋 View all blocked usernames
* ➕ Ban usernames directly from the Velocity console
* ➖ Unban usernames directly from the Velocity console
* ⚡ Lightweight and dependency-free

## Commands

All commands are **console-only**.

| Command                | Description                            |
| ---------------------- | -------------------------------------- |
| `/sp ban <username>`   | Ban a username                         |
| `/sp unban <username>` | Remove a username from the ban list    |
| `/sp list`             | List all banned usernames              |
| `/sp reload`           | Reload `config.toml` and `blocked.txt` |
| `/sp help`             | Show available commands                |

`/serverprotect` can also be used instead of `/sp`.

## Configuration

After the first startup, ServerProtect creates:

```text
plugins/
└── serverprotect/
    ├── config.toml
    └── blocked.txt
```

### `config.toml`

The kick message uses **MiniMessage**.

You can use MiniMessage tags such as:

```text
<red>
<green>
<blue>
<gray>
<dark_red>
<bold>
<italic>
<underlined>
<gradient:red:dark_red>
<newline>
```

### `blocked.txt`

Add one username per line:

```text
# One username per line
Player123
BadPlayer
ExampleUser
```

Username matching is **case-insensitive**.

For example, banning:

```text
Player123
```

also blocks:

```text
player123
PLAYER123
pLaYeR123
```

## How It Works

When a player attempts to connect:

```text
Player
   │
   ▼
Velocity PreLoginEvent
   │
   ▼
Check blocked.txt
   │
   ├── Not blocked ──► Continue login
   │
   └── Blocked ──────► Kick with MiniMessage
```

Because the check happens during `PreLoginEvent`, the player is rejected by the **Velocity proxy before reaching a backend server**.

## Example

Ban a player:

```text
/sp ban ExamplePlayer
```

Output:

```text
Banned ExamplePlayer.
```

Check the list:

```text
/sp list
```

Unban:

```text
/sp unban ExamplePlayer
```

Reload after manually editing the files:

```text
/sp reload
```

