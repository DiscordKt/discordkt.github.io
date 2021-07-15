In some cases, you may need to collect a lot of information from a user, which makes using commands less feasible.
This is where the conversation DSL comes in. It can be used to collect information over many messages instead.
Once you start a conversation, the bot will ask a series of questions to a target user and gather the responses.
Here is an example conversation:

```kotlin
fun demoConversation() = conversation(exitString = "exit") {
    val name = promptMessage(AnyArg, "What is your name?")
    val age = promptMessage(IntegerArg, "How old are you?")

    respond("Nice to meet you $name! $age is a great age.")
}
```

This DSL uses coroutines to prompt for values in "real time" as the conversation is executed. This means that you can process the input immediately after your prompt.

## Input

To get input from a user, there are several functions you can use. Most of these blocks accept an `ArgumentType`, just like a command. This is the type of data you're trying to produce. If the user's answer is not parsed successfully, the prompt will be sent again.

### Text prompt
```kotlin
val age = promptMessage(IntegerArg, "What is your age?")
```

### Validating prompt
```kotlin
val age = promptUntil(
    argumentType = IntegerArg,
    prompt = "What is your age?",
    error = "Age must be positive!",
    isValid = { it > 0 }
)
```

### Embed prompt
```kotlin
val age = promptEmbed(IntegerArg) {
    title = "What is your age?"
}
```

### Button prompt
```kotlin
val response = promptButton<String> {
    embed {
        title = "Do you like DiscordKt?"
        color = Color(0x00bfff)
    }

    buttons {
        button("Yes", Emojis.whiteCheckMark, "Glad you like it")
        button("No", Emojis.x, "You should let me know how to fix the lib.")
    }
}
```

## Starting a conversation

Once a conversation function is written, you call it to receive your `Conversation`. From this, you can start it publicly (in a guild) or privately (in a DM).

```kotlin
val result = demoConversation().startPublicly(discord, author, channel)
```
```kotlin
val result = demoConversation().startPrivately(discord, author)
```

Both of these functions return a `ConversationResult` indicating the outcome of the conversation.
