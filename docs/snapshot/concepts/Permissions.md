When making more complicated bots, you may need to restrict commands to only be run by certain users or roles. To manage command permissions, DiscordKt provides the `PermissionSet` interface.

## Configuration

```kotlin
object Permissions : PermissionSet {
    val BOT_OWNER = permission("Bot Owner") { users(discord.getInjectionObjects<Configuration>().botOwner) }
    val GUILD_OWNER = permission("Guild Owner") { users(guild!!.ownerId) }
    val EVERYONE = permission("Everyone") { roles(guild!!.everyoneRole.id) }

    override val hierarchy: List<Permission> = listOf(EVERYONE, GUILD_OWNER, BOT_OWNER)
    override val commandDefault: Permission = EVERYONE
}
```

This can be viewed in three main parts:

- The permissions
- The hierarchy
- The default

The permissions are declared first (`BOT_OWNER`, `GUILD_OWNER`, `EVERYONE`), by using the `permission` builder. This has two functions, `users` and `roles` which state who is allowed to use a command per guild.

The `hierarchy` is what determines the order of permissions. Your lowest permission level should be at the beginning, through your highest at the end. A user can run any command less than or equal to their permission level.

The `commandDefault` is the default permission required to run any command. This can be overridden at a category or command level. See the usage section below

## Registering

Once created, your custom PermissionSet must be registered in the main bot function via the `configure` block.

```kotlin
configure {
    permissions = Permissions
}
```

## Usage

To set the required permission by category, pass the desired permission level into the `commands` builder.

```kotlin
fun botOwnerCommands() = commands("BotOwner", Permissions.BOT_OWNER) { ... }
```

This will set the required permission of each command to this value. You can also set it directly in each command. The most narrowly set value will be used (Command > Category > Default).

```kotlin
command("BotOwner") {
    description = "Command requiring BOT_OWNER permissions"
    requiredPermission = Permissions.BOT_OWNER
    execute {
        respond("Hello bot owner!")
    }
}
```
