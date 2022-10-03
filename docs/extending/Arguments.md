To make a custom argument, we implement one of the `Argument` sub-interfaces. Slash commands currently accept 8 types of
input; 4 primitives and 4 Discord entities. Each has a class representation:

* `StringArgument`, `IntegerArgument`, `DoubleArgument`, `BooleanArgument`
* `UserArgument`, `RoleArgument`, `ChannelArgument`, `AttachmentArgument`

For this example we will extend a basic String input:

```kotlin
open class HexColorArg(override val name: String = "Color",
                       override val description: String = "A hexadecimal color") : StringArgument<Color> {
    companion object : HexColorArg()

    override suspend fun transform(input: String, context: DiscordContext): Result<Color> {
        if (input.length !in 6..7) return Error(internalLocale.invalidFormat)

        val trimmedInput = input.takeLast(6).uppercase()
        val isValidHex = trimmedInput.all { it in '0'..'9' || it in 'A'..'F' }

        if (!isValidHex)
            return Error(internalLocale.invalidFormat)

        return Success(Color(trimmedInput.toInt(16)))
    }

    override suspend fun generateExamples(context: DiscordContext): List<String> = listOf(stringify(Color((0..255).random(), (0..255).random(), (0..255).random())))
}
```

### Class Stub

The class name for every argument should reflect the type of data you're trying to accept, followed by `Arg`. You then
extend the appropriate `Argument` subtype, providing it the type that you want this argument to produce. Since we want
our StringArgument to produce Colors from the input, we use `StringArgument<Color>`.

### Parameters

The first parameter in every Argument is the name. This is what the arg will be displayed as when prompting the user for
slash input. This displays the argument as "Hex" instead of the default "Color": `HexColorArg("Hex")`

The second argument is the description, which is also shown during the prompt. All args provided by DiscordKt, but it is
encouraged to override this to be specific to your usage in the command. `HexColorArg("Hex", "Your favorite color")`

### Companion Object

The companion object for an Argument is just syntactic sugar when using the argument. This companion object allows you
to use an Argument by name instead of having to invoke the constructor. `execute(HexColorArg)` instead
of `execute(HexColorArg())`.

### Examples

Examples are used primarily for help menus. When help is invoked on a command, an example from each Argument is selected
at random. The `generateExamples` function helps you generate relevant examples on the fly using the `DiscordContext`.

### Result

Each Argument must return a `Result` that matches the type expected by the argument. So in this case, we
use `Result<Color>` as our return type. The actual return can either be `Success` or `Error`:

- `Error` - The parsing has failed. The input args could not be converted to the required type. The String provided will
  be sent as a message in the channel where the command was invoked.
- `Success` - The parsing was successful. The input is consumed and the required type is returned.

### Transform

The `transform` function is the logic behind every Argument. This is what converts the user input into the desired type.
It accepts the following:

input: String, context: DiscordContext

- `input: T` - This is the user input to the command. The type is based on the type of Argument you accept.
- `context: DiscordContext` - This is the Discord invocation context in cases where you need that to perform your
  transformation.
