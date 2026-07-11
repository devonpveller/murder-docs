# Command

**Namespace:** Murder.Diagnostics \
**Assembly:** Murder.dll

```csharp
sealed struct Command
```

Represents a parsed in-game console command, pairing the method to invoke with its name, help text, and expected arguments.

**Intent:** Stores all metadata needed to dispatch a console command at runtime.

**Use-case:** Populated automatically by `CommandServices` through reflection; accessed when the player types a command in the debug console.

### ⭐ Properties
#### Arguments
```csharp
public ValueTuple`2[] Arguments { get; public set; }
```
Ordered list of `(type, name)` pairs describing the parameters the command expects.

**Returns** \
[ValueTuple\<T1, T2\>[]](https://learn.microsoft.com/en-us/dotnet/api/System.ValueTuple-2?view=net-7.0) \
#### Help
```csharp
public string Help { get; public set; }
```
Human-readable description shown in the console when the user types `help`.

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
#### Method
```csharp
public MethodInfo Method { get; public set; }
```
The reflected static method that will be invoked when this command is executed.

**Returns** \
[MethodInfo](https://learn.microsoft.com/en-us/dotnet/api/System.Reflection.MethodInfo?view=net-7.0) \
#### Name
```csharp
public string Name { get; }
```
The command keyword as it appears in the console (taken from the method name, lowercased).

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \


⚡