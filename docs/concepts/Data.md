It is often necessary to write data to persistent storage. This is commonly used for configuration files, so that will be our example.

## Creating

```kotlin
@Serializable
data class BotConfiguration(var prefix: String = "!") : Data()
```

The core of any `Data` is first a Kotlin `data class`. This is where you will add your configuration options and persistent data. To be detected correctly, you must also extend `Data`.
DiscordKt uses Kotlin's serialization engine, which means your `Data` class must be annotated with `@Serializable` to be serialized properly. You will also need to add the kotlin serialization plugin to your build file.

## Registering

To be loaded into DiscordKt, a `Data` class is passed into a loading function in the `bot` block

```kotlin
bot(token) {
    val configuration = data("config/config.json") { Configuration() }
}
```

The `data` loading function takes a file path and a default value. The path is where the `Data` is saved/loaded on disk. When running the program for the first time, there will be nothing to load from the disk. This is where the default value comes in. On following runs, the configuration from the disk is loaded. Either way, you are guaranteed an instance of your class in the `bot` block. This can be used immediately to access your configuration options (or whatever data you have).

## Editing

No matter what type of data you're storing, you will often need to make changes to these objects during runtime. This includes writing the updated version of the object to the file. DiscordKt provides a unified function for these 2 operations.

```kotlin
configuration.edit { prefix = newPrefix }
```

This function will edit the live configuration object, while also writing these changes to disk.
