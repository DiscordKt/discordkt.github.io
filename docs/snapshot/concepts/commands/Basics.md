To register commands using DiscordKt, create a function that calls the `commands` builder. This builder accepts the name of the category and can contain as many commands as you want.

```kotlin
fun utilityCommands() = commands("Utility") {
    command("Ping") {
        description = "Check to see if the bot is online."
        execute {
            respond("Pong!")
        }
    }
}
```

This code creates a category with the name `Utility` and a single command named `Ping`. This command is also provided a description, which will be visible whenever someone invokes `help` on the command, as well as written into the automatic documentation.

### Invoking Commands
Assuming that your bot is configured with the prefix `+`, you can now invoke your command with `+ping`. This will trigger the `execute` function, which is the action block of all commands.
