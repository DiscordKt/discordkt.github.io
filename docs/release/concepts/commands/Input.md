Accepting input into a command can be done using arguments. Arguments in DiscordKt are defined as an `ArgumentType`. An ArgumentType's job is to parse the raw input to a command and turn it into something that you can use, or to report failure if this parsing cannot be completed successfully. Here is an example of a command that accepts some arguments.

```kotlin
command("Add") {
    description = "Add two numbers together."
    execute(IntegerArg, IntegerArg) {
        val first = args.first
        val second = args.second

        respond("${first + second}")
    }
}
```

ArgumentTypes are accepted into the execute function of a command. This command takes in two `IntegerArg` arguments, but you can accept any number of arguments of any type.

The action block of the execute function now has access to this input. This input is type-inferred based on the ArgumentType, so there is no need to cast. Since the command accepts two IntegerArgs, the type for our variables (`first` and `second`) will be `Int`. Parsing and validation are handled by the ArgumentType itself. DiscordKt will not allow any values that don't pass the checks provided by the specific ArgumentType.

This command will fail to execute if the input is anything except exactly two integers.
