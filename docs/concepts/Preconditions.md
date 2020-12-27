## Preconditions

Preconditions are a way to validate state before you begin to process a command. You have access to the CommandEvent, from which you can access who invoked the command, where it was invoked, etc.

```kotlin
fun botPrecondition() = precondition {
    if (author.isBot)
        fail("Bots cannot do this!")
}
```

This code checks whether or not the user who attempted to invoke a command is a bot. If it is, the precondition will fail. All preconditions must be passed in order for a command to be run.

If a precondition is failed, the String passed into `fail` will be sent as a message in the channel where the command was attempted.
