To make a custom argument, we implement the `Argument` interface. The provided `IntegerArg` will be used for this example.

```kotlin
open class IntegerArg(override val name: String = "Integer",
                      override val description: String = "A whole number") : Argument<Int> {

    companion object : IntegerArg()

    override suspend fun convert(arg: String, args: List<String>, event: CommandEvent<*>): ArgumentResult<Int> =
        when (val result = arg.toIntOrNull()) {
            null -> Error(internalLocale.invalidFormat)
            else -> Success(result)
        }

    override suspend fun generateExamples(event: CommandEvent<*>): List<String> = (0..10).map { it.toString() }
}
```

### Class Stub
The class name for every argument should reflect the type of data you're trying to accept, followed by `Arg`. You then extend `Argument`, providing it the type that you want this argument to produce. Since we want our IntegerArg to produce integers from the string input, we use `Argument<Int>`.

### Parameters
The first parameter in every Argument is the name. This is what the arg will be displayed as in help menus, and in the automatic documentation. The following example displays the argument as "Index" instead of the default "Integer": `IntegerArg("Index")`

### Companion Object
The companion object for an Argument is just syntactic sugar when using the argument. This companion object allows you to use an Argument by name instead of having to invoke the constructor. `execute(IntegerArg)` instead of `execute(IntegerArg())`.

### Examples
Examples are used primarily for help menus. When help is invoked on a command, an example from each Argument is selected at random. The `generateExamples` function helps you generate relevant examples on the fly using the CommandEvent.

### ArgumentResult
Each Argument must return an `ArgumentResult` that matches the type expected by the argument. So in this case, we use `ArgumentResult<Int>` as our return type. The actual return can either be `Success` or `Error`:

- `Error` - The parsing has failed. The input could not be converted to the required type. The provided String will be sent as a message in the channel where the command was invoked.
- `Success` - The parsing was successful. The input is consumed and the required type is returned.

### Convert
The convert function is the logic behind every Argument. This is what converts the user input into the desired type. It accepts the following:

- `arg: String` - This is the relevant argument passed into the command. As each Argument is processed, args are consumed from the list.
- `args: List<String>` - This list contains all of the remaining arguments passed into a command.
- `event: CommandEvent<*>` - This is the invocation event for the command.
