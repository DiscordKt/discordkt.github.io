To make a custom argument, we implement the `ArgumentType` interface. The provided `IntegerArg` will be used for this example.

```kotlin
open class IntegerArg(override val name: String = "Integer") : ArgumentType<Int> {
    companion object : IntegerArg()

    override val description = "A whole number"

    override suspend fun convert(arg: String, args: List<String>, event: CommandEvent<*>): ArgumentResult<Int> {
        val result = arg.toIntOrNull() ?: return Error("Invalid format")
        return Success(result)
    }

    override suspend fun generateExamples(event: CommandEvent<*>) = (0..10).map { it.toString() }
}
```

### Class Stub
The class name for every argument should reflect the type of data you're trying to accept, followed by `Arg`. You then extend `ArgumentType`, providing it the type that you want this argument to produce. Since we want our IntegerArg to produce integers from the string input, we use `ArgumentType<Int>`.

### Parameters
The first parameter in every ArgumentType is the name. This is what the arg will be displayed as in help menus, and in the automatic documentation. This displays the argument as "Index" instead of the default "Integer": `IntegerArg("Index")`

### Companion Object
The companion object for an ArgumentType is just syntactic sugar when using the argument. This companion object allows you to use an ArgumentType by name instead of having to invoke the constructor. `execute(IntegerArg)` instead of `execute(IntegerArg())`.

### Examples
Examples are used primarily for help menus. When help is invoked on a command, an example from each ArgumentType is selected at random. The `generateExamples` function helps you generate relevant examples on the fly using the CommandEvent.

### ArgumentResult
Each ArgumentType must return an `ArgumentResult` that matches the type expected by the argument. So in this case, we use `ArgumentResult<Int>` as our return type. The actual return can either be `Success` or `Error`:

- `Error` - The parsing has failed. The input args could not be converted to the required type. The String provided will be sent as a message in the channel where the command was invoked.
- `Success` - The parsing was successful. The input is consumed and the required type is returned.

### Convert
The convert function is the logic behind every ArgumentType. This is what converts the user input into the desired type. It accepts the following:

- `arg: String` - This is the relevant argument passed into the command. As each ArgumentType is processed, args are consumed from the list.
- `args: List<String>` - This list contains all of the remaining arguments passed into a command.
- `event: CommandEvent<*>` - This is the invocation event for the command.
