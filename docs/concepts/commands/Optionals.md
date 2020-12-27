Some commands might not need all the input all the time. This

```kotlin
command("DisplayText") {
    description = "Display some text."
    execute(AnyArg.optional("Hello")) {
        val text = args.first
        respond("Your text is: $text")
    }
}
```

This accepts an optional `AnyArg`, meaning the command can be called with 0 or 1 arguments. The `optional` function can be called on any `ArgumentType`. The provided default value will be used if no input is provided by the user. In this case, when called with no arguments, the value of the text is `"Hello"`.
