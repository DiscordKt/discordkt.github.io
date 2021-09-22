To check if a user has permission to execute a command, you can create a permission hierarchy with an enum.
Your highest permission level should be at the top, and the lowest at the bottom.
This enum must implement `PermissionSet`.

```kotlin
enum class Permissions : PermissionSet {
    BOT_OWNER {
        override suspend fun hasPermission(context: PermissionContext) = context.user.id.value == 298168112824582154
    },
    GUILD_OWNER {
        override suspend fun hasPermission(context: PermissionContext) = context.getMember()?.isOwner() ?: false
    },
    EVERYONE {
        override suspend fun hasPermission(context: PermissionContext) = true
    }
}
```

Once created, we must integrate it.
Firstly, it must be registered in the main bot function via the `configure` block.

```kotlin
configure {
    permissions(commandDefault = Permissions.EVERYONE)
}
```

This registers the permission enum we created and sets the permission level of every command to `EVERYONE`.
To override this value, simply specify it in the target command.

```kotlin
command("BotOwner") {
    description = "Command requiring BOT_OWNER permissions"
    requiredPermission = Permissions.BOT_OWNER
    execute {
        respond("Hello bot owner!")
    }
}
```

To set the required permission by category, pass the desired permission level into the `commands` builder.

```kotlin
fun botOwnerCommands() = commands("BotOwner", Permissions.BOT_OWNER) { ... }
```

This sets each command in this category to `BOT_OWNER`, which can then be overridden on a per-command basis as shown above.
