Slash Commands are the new way of interacting with bots on discord. A user can discover these commands by pressing `/` and then recieve help with running it right from the discord UI.

## Creating

To create slash commands, the syntax is identical to creating a text command, you just need to use the `slash` builder instead.

```kotlin
slash("Hello") {
    description = "A Hello World command"
    execute {
        respond("Hello World!")
    }
}
```

## Input

Input is accepted to a slash command in the same way that you would for a simple text command.

```kotlin
slash("SlashAdd") {
    description = "A simple addition command"
    execute(IntegerArg("First"), IntegerArg("Second")) {
        val (first, second) = args
        respond("$first + $second = ${first + second}")
    }
}
```

Slash commands will also be automatically registered as text commands as well.