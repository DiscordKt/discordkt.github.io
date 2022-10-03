Each `Argument` provided to a command can be made optional with either `optional` or `optionalNullable` functions.

```kotlin
slash("DisplayText", "Display some text.") {
    execute(AnyArg.optional("Hello")) {
        val text = args.first
        respond("Your text is: $text")
    }
}
```

This command accepts an optional `AnyArg`, meaning the command can be called with 0 or 1 arguments. The provided default value will be used if no input is provided by the user. In this case, when called with no arguments, the value of the text is `"Hello"`.
