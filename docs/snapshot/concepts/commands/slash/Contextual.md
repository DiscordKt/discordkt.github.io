Discord provides a new type of slash commands that will show up in context menus. Right clicking on a user or message will open the normal context menu, but now with an added `Apps` category. This is where your contextual apps will live.

## Creating

Contextual commands will be registered automatically if applicable, there is no specialized builder, just use `slash`. The second arg to this builder is `appName`, which is the text that will show up when using these contextual commands. The first arg (`name`) will be used to register this command as a normal slash command and a discordkt text command.

## User

A user command is any slash command that accepts solely a `UserArg` or `MemberArg`.

```kotlin
slash("Info", appName="Show User Info") {
    description = "Get information for the target user"
    execute(UserArg) {
        respond(args.first.descriptor())
    }
}
```

## Message

A message command is any slash command that accepts solely a `MessageArg`.

```kotlin
slash("Link", appName="Get Message Link") {
    description = "Get a message's jump link"
    execute(MessageArg) {
        respond(args.first.jumpLink() ?: "<Unknown Link>")
    }
}
```