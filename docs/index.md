<p align="center">
  <a href="https://github.com/DiscordKt/DiscordKt">
    <img alt="DiscordKt" src="https://img.shields.io/badge/DiscordKt-00bfff?style=flat-square">
  </a>

  <a href="https://github.com/DiscordKt/ExampleBot">
    <img alt="ExampleBot" src="https://img.shields.io/badge/Example%20Bot-00bfff?style=flat-square">
  </a>
</p>

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
