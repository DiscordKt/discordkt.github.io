It is often necessary to write data to persistent storage. This is commonly used for configuration files that are read on startup.

```kotlin
class BotConfiguration(val prefix: String = "!") : Data("config/config.json", killIfGenerated = false)
```

Any class that extends from `Data` will be created and written to a file at the `path` location if it does not already exist. If the file already exists, it will be deserialized into an instance and injected.

If the target file does not exist, it will be generated with the default values provided. If `killIfGenerated` is true, the program will generate the file, then exit.
