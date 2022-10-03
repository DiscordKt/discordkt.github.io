Accepting input into a command can be done using an `Argument`. An Argument's job is to transform the command input into something that you can use, or to report failure if this transformation cannot be completed successfully. Here is an example of a command that accepts some arguments.

```kotlin
slash("Plus", "A simple addition command") {
    execute(IntegerArg("First"), IntegerArg("Second")) {
        val (first, second) = args
        respond("$first + $second = ${first + second}")
    }
}
```

Arguments are accepted into the execute function of a command. This command takes in two `IntegerArg` arguments, but you can accept any number of arguments of any type.

The action block of the execute function now has access to this input. This input is type-inferred based on the Argument, so there is no need to cast. Since the command accepts two IntegerArgs, the type for our variables (`first` and `second`) will be `Int`. Parsing and validation are handled by the Argument itself. DiscordKt will not allow any values that don't pass the checks provided by the specific Argument.
