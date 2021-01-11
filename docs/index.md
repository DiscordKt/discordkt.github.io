DiscordKt is a Kotlin Discord library, built on top of [Kord](https://github.com/kordlib/kord) - a Kotlin Discord API.

### Installation

=== "build.gradle.kts"
    ```kotlin
    dependencies {
        implementation("me.jakejmattson:DiscordKt:0.21.3")
    }
    ```

=== "build.gradle"
    ```groovy
    dependencies {
        implementation 'me.jakejmattson:DiscordKt:0.21.3'
    }
    ```

=== "pom.xml"
    ```xml
    <dependency>
        <groupId>me.jakejmattson</groupId>
        <artifactId>DiscordKt</artifactId>
        <version>0.21.3</version>
    </dependency>
    ```

### Starting up
The start up procedure for DiscordKt is very simple, you just need to provide the token in order to get going.

```kotlin
fun main(args: Array<String>) {
    val token = "your-bot-token"

    bot(token) {
      prefix { "+" }
    }
}
```
