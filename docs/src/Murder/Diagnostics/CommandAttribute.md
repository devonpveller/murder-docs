# CommandAttribute

**Namespace:** Murder.Diagnostics \
**Assembly:** Murder.dll

```csharp
public class CommandAttribute : Attribute
```

Marks a static method as an in-game debug console command and supplies the help text shown in `help`.

**Intent:** Decorates static methods in `ICommands` implementors so `CommandServices` can discover them via reflection and expose them in the debug console.

**Use-case:** Apply `[Command("Does X to entity Y")]` to any static method in a class that implements `ICommands` to make it callable from the in-game console.

**Implements:** _[Attribute](https://learn.microsoft.com/en-us/dotnet/api/System.Attribute?view=net-7.0)_

### ⭐ Constructors

```csharp
public CommandAttribute(string help)
```

Creates the attribute with the given help text that will be shown in the console.

**Parameters** \
`help` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

### ⭐ Properties

#### Help

```csharp
public readonly string Help;
```

The help string displayed next to this command when the user types `help` in the console.

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### TypeId

```csharp
public virtual Object TypeId { get; }
```

Unique object identity for this attribute type, inherited from `Attribute`.

**Returns** \
[Object](https://learn.microsoft.com/en-us/dotnet/api/System.Object?view=net-7.0) \

⚡
