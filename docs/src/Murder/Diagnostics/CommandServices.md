# CommandServices

**Namespace:** Murder.Diagnostics \
**Assembly:** Murder.dll

```csharp
public static class CommandServices
```

Discovery and dispatch hub for all in-game debug console commands.

**Intent:** On first use, reflects over every loaded assembly to find static classes that implement [ICommands](../../Murder/Diagnostics/ICommands.html) and collect their `[Command]`-attributed static methods into a name-indexed lookup table (`Command` records). It then owns the job of parsing raw text typed into the debug console, matching it to a discovered command, converting the typed arguments to the method's parameter types, and invoking it.

**Use-case:** Called from the debug console UI (`GameLogger`'s console overlay) each time the player presses enter: `CommandServices.Parse(world, input)` returns the string to print as the console's response — either the command's own output, the `help` listing, or an error message describing what went wrong. Game code that wants to add new debug commands does not call into `CommandServices` directly; instead it defines a static class implementing `ICommands` with `[Command("...")]`-decorated static methods (whose first parameter must be `World`), and `CommandServices` picks them up automatically the first time `AllCommands`/`Parse` is touched.

### ⭐ Properties

#### AllCommands

```csharp
public static ImmutableDictionary<string, Command> AllCommands { get; }
```

The full set of discovered commands, keyed by their lowercase console name (case-insensitively). Built once via a `Lazy<T>` the first time it — or `Parse` — is accessed, then reused for the rest of the process's lifetime; new `ICommands` methods added after that point (e.g. via hot-reload) will not be picked up without a process restart.

**Returns** \
[ImmutableDictionary\<string, Command\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableDictionary-2?view=net-7.0) \

### ⭐ Methods

#### Parse(World, string)

```csharp
public static string Parse(World world, string input)
```

Parses one line of console input and dispatches it: `"help"` returns the full command listing; an empty or unrecognized input returns an "unable to recognize command" message; otherwise the first whitespace-separated token is looked up in `AllCommands` and, if found, its remaining tokens are converted to the command method's parameter types (via `Convert.ChangeType`, with a trailing `f` trimmed for `float` arguments) and the method is invoked with `world` as its first argument. Argument-count or type-conversion failures return a usage message instead of throwing.

**Parameters** \
`world` [World](../../Bang/World.html) \
`input` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

⚡
