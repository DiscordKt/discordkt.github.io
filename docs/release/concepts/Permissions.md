When making more complicated bots, you may want or need to restrict commands to only be run by certain users or roles.
Discord provides a built-in way for server owners to change the slash command permissions of your bot, but you do need
to set a default permission level.

Permissions are defined by vanilla Discord permissions. For example, to make a command only available if the user has
the "Manage Messages" permission, you'd define the permission object as `Permissions(Permission.ManageMessages)`. You
can also combine permissions by specifying more than one in the constructor, for example
`Permissions(Permission.ManageMessages, Permission.ManageNicknames)`. In this case, **both** the "Manage Messsages" and
the "Manage Nicknames" permissions are needed.

## Global permission level

If you want, you can set a default permission level for all registered commands. This is done in the bot's `configure`
block.

```kotlin
configure {
    defaultPermissions = Permissions(Permission.UseApplicationCommands)
}
```

## Category permission level

You can also specify a permission level for a category. To do this, you need to pass the desired permissions in the
`commands` builder.

```kotlin
fun adminCommands() = commands("Administration", requiredPermissionLevel = Permissions(Permission.Administrator)) {
    // ...
}
```

## Command permission level

Lastly, you can also set the permission level directly in the command.

```kotlin
slash("ban") {
    requiredPermissions = Permissions(Permission.BanMembers)
    execute(UserArg) {
        args.first.asMemberOrNull(guild.id)?.ban()
    }
}
```

The narrowest permission level will be the permission level for a command (global > category > command).
