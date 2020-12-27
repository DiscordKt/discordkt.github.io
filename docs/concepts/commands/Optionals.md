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

This accepts an optional `AnyArg`, meaning the command can be called with 0 or 1 arguments.

The `optional` function can be called on any `ArgumentType`. We then provide a default value as a fallback if none is provided by the user. This default value is also type-safe, meaning that the type of default must match the output of the ArgumentType.

In this case, when called with no arguments, the value of the text is `"Hello"`.
