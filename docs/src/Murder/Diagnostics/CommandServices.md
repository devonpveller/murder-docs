# CommandServices

**Namespace:** Murder.Diagnostics \
**Assembly:** Murder.dll

```csharp
public static class CommandServices
```

Discovery and dispatch hub for all in-game debug console commands.

**Intent:** Collects all static methods decorated with `[Command]` from types that implement `ICommands`, and parses console input to invoke the matching method.

**Use-case:** Call `CommandServices.Parse(world, input)` from the debug console UI to execute the command the player typed.

### ⭐ Properties
#### AllCommands
```csharp
public static ImmutableDictionary<TKey, TValue> AllCommands { get; }
```
Lazy-initialized dictionary mapping command names to their `Command` metadata, built once from reflection.

**Returns** \
[ImmutableDictionary\<TKey, TValue\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableDictionary-2?view=net-7.0) \
### ⭐ Methods
#### Parse(World, string)
```csharp
public string Parse(World world, string input)
```
Parses the console input string and dispatches the matching command, returning its output or an error message.

**Parameters** \
`world` [World](../../Bang/World.html) \
`input` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \



⚡