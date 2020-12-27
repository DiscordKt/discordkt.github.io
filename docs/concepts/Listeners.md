To listen for Discord events, DiscordKt provides the `listeners` builder, where you can call `on<Event>`.

```kotlin
fun demoListeners() = listeners {
    on<MessageCreateEvent> {
        println(message.content)
    }
}
```

This block listens for a single event `MessageCreateEvent` and prints the content of the message.
