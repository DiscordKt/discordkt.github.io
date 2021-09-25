DiscordKt is a Kotlin Discord library, built on top of [Kord](https://github.com/kordlib/kord) - a Kotlin Discord API. For full documentation, you must choose a branch.

#### [Release](release/index.md)
A stable, unchanging version.

#### [Snapshot](snapshot/index.md)
A live snapshot with the most recent features.

## Syntax Samples

Below are some syntax samples for the library.

#### Startup

```kotlin
fun main(args: Array<String>) {
    val token = "your-bot-token"

    bot(token) {
      prefix { "+" }
    }
}
```

#### Commands

```Kotlin
fun demo() = commands("Demo") {
    command("Hello") {
        description = "A 'Hello World' command."
        execute {
            respond("Hello World!")
        }
    }

    command("Add") {
        description = "Add two numbers together."
        execute(IntegerArg, IntegerArg) {
            val (first, second) = args
            respond(first + second)
        }
    }
}
```

#### Events

```Kotlin
fun testListeners() = listeners {
    on<MessageCreateEvent> {
        println(message.content)
    }
}
```
