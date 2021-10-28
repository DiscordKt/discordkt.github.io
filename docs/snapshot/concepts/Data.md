It is often necessary to write data to persistent storage. This is commonly used for configuration files that are read on startup.

The class needs to be marked with `@Serializable` to allow it to be serialized properly.

```kotlin
@Serializable
data class MyConfig(val value: String) : Data()
```

To read the data back simply call the data function inside the bot DSL block, a fallback must be defined for how to construct
the data if the file isn't located.

```kotlin
// main
bot(token) {
    val config = data("./config.json") {
        MyConfig("example")    
    }
}
```

If the path does not exist it will be created, if the file does not exist the default value will be saved to a new file.