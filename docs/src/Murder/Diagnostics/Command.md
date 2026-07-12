# Command

**Namespace:** Murder.Diagnostics \
**Assembly:** Murder.dll

```csharp
public readonly struct Command
```

Nested inside [CommandServices](../../Murder/Diagnostics/CommandServices.html) (`CommandServices.Command`), this is the reflection-built metadata record for a single in-game debug console command: which method to call, what its parameters look like, and the help text to show for it.

**Intent:** Gives `CommandServices` a lightweight, immutable snapshot of everything needed to validate and invoke a `[Command]`-decorated method without re-running reflection lookups on every console keystroke. One `Command` value is created per discovered method and cached for the lifetime of the process.

**Use-case:** You never construct a `Command` yourself. `CommandServices` builds the entire set once (via `FetchAllCommands`) by scanning every loaded assembly for static classes implementing [ICommands](../../Murder/Diagnostics/ICommands.html) and collecting their `[Command]`-attributed methods; the result is exposed read-only through `CommandServices.AllCommands`. Game or tooling code that wants to introspect available console commands (e.g. to build an autocomplete list) can enumerate that dictionary and read `Name`/`Help`/`Arguments` from each `Command`.

### ⭐ Properties

#### Arguments

```csharp
public (Type Type, string Name)[] Arguments { get; init; }
```

The command method's parameters, captured as `(Type, Name)` pairs in declaration order. By convention the first entry is always `(typeof(World), "world")`, since every command method takes the current [World](../../Bang/World.html) as its first argument; `CommandServices.ExecuteCommand` uses the remaining entries to convert the player's typed tokens to the correct types via `Convert.ChangeType` before invoking `Method`.

**Returns** \
[ValueTuple\<Type, string\>[]](https://learn.microsoft.com/en-us/dotnet/api/System.ValueTuple-2?view=net-7.0) \

#### Help

```csharp
public string Help { get; init; }
```

The help string supplied to the method's `[Command("...")]` attribute, shown next to the command's usage line when the player types `help` in the debug console.

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### Method

```csharp
public MethodInfo Method { get; init; }
```

The reflected static method that implements this command. `CommandServices.ExecuteCommand` invokes it with `null` as the target (since it must be `static`) and the converted argument array as parameters; the method's return value (a `string`, or `null`) is written back to the console as the command's output.

**Returns** \
[MethodInfo](https://learn.microsoft.com/en-us/dotnet/api/System.Reflection.MethodInfo?view=net-7.0) \

#### Name

```csharp
public string Name { get; }
```

The keyword the player types to invoke this command. Derived from `Method.Name` with the first character lowercased (e.g. a method named `GodMode` becomes the console keyword `godMode`); this is also the key used for lookups in `CommandServices.AllCommands`, matched case-insensitively.

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

⚡
