DiscordKt is a Kotlin Discord library, built on top of [Kord](https://github.com/kordlib/kord) - a Kotlin Discord API.

=== "build.gradle.kts"
    ```kotlin
    dependencies {
        implementation("me.jakejmattson:DiscordKt:0.23.4")
    }
    ```
    
=== "build.gradle"
    ```groovy
    dependencies {
        implementation 'me.jakejmattson:DiscordKt:0.23.4'
    }
    ```
    
=== "pom.xml"
    ```xml
    <dependencies>
        <dependency>
            <groupId>me.jakejmattson</groupId>
            <artifactId>DiscordKt</artifactId>
            <version>0.23.4</version>
        </dependency>
    </dependencies>
    ```

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
    slash("Hello", "A 'Hello World' command.") {
        execute {
            respond("Hello World!")
        }
    }

    slash("Add", "Add two numbers together.") {
        execute(IntegerArg("First"), IntegerArg("Second")) {
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