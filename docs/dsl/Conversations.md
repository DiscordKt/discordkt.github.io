In some cases, you may need to collect a lot of information from a user, which makes using commands less feasible.
This is where the conversation DSL comes in. It can be used to collect information over many messages instead.
Once you start a conversation, the bot will ask a series of questions to a target user and gather the responses.
Here is an example conversation:

```kotlin
fun demoConversation() = conversation(exitString = "exit") {
    val name = promptMessage(AnyArg, "Please enter your name.")
    val age = promptMessage(IntegerArg, "Please enter your age.")

    respond("Nice to meet you $name! $age is a great age.")
}
```

This DSL uses coroutines to prompt for values in "real time" as the conversation is executed. This means that you can process the input immediately after your prompt.

## Input

To get input from a user, there are several functions you can use. Most of these blocks accept an `ArgumentType`, just like a command. This is the type of data you're trying to produce. If the user's answer is not parsed successfully, the prompt will be sent again.

### A simple string prompt
```kotlin
val age = promptMessage(IntegerArg, "Please enter your age.")
```

### A validating prompt
```kotlin
val age = promptUntil(
    argumentType = IntegerArg,
    prompt = "Please enter your age.",
    error = "Age must be positive!",
    isValid = { it > 0 }
)
```

### An embed as a prompt
```kotlin
val age = promptEmbed(IntegerArg) {
    title = "What is your age?"
}
```

### An embed with reactions
```kotlin
val response = promptReaction(
    PromptedReaction(Emojis.whiteCheckMark, "Yes it's great!", "Glad you like the lib."),
    PromptedReaction(Emojis.x, "Not a fan.", "You should let me know how to fix the lib.")
) {
    title = "Do you like DiscordKt?"
    color = Color(0x00bfff)
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
