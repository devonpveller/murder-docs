# Fact

**Namespace:** Murder.Core.Dialogs \
**Assembly:** Murder.dll

```csharp
public sealed struct Fact
```

Identifies a named, typed blackboard variable within a specific blackboard scope.

**Intent:** Acts as a key that uniquely addresses one variable in the blackboard system — specifying which blackboard holds it, its name, and its data type (`FactKind`).

**Use-case:** Embed a `Fact` inside a `Criterion` or `DialogAction` to target a specific blackboard variable for reading or writing during dialogue evaluation.

### ⭐ Constructors

```csharp
public Fact()
```

Creates an empty, invalid fact (`FactKind.Invalid`).

```csharp
public Fact(string blackboard, string name, FactKind kind, Type componentType)
```

Creates a fully-specified fact targeting the named variable in the given blackboard.

**Parameters** \
`blackboard` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
`name` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
`kind` [FactKind](../../../Murder/Core/Dialogs/FactKind.html) \
`componentType` [Type](https://learn.microsoft.com/en-us/dotnet/api/System.Type?view=net-7.0) \

```csharp
public Fact(Type componentType)
```

Creates a `FactKind.Component` fact targeting the specified component type.

**Parameters** \
`componentType` [Type](https://learn.microsoft.com/en-us/dotnet/api/System.Type?view=net-7.0) \

### ⭐ Properties

#### Blackboard

```csharp
public readonly string Blackboard;
```

If null, grab the default blackboard.

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### ComponentType

```csharp
public readonly Type ComponentType;
```

Set when the fact is of type [FactKind.Component](../../../Murder/Core/Dialogs/FactKind.html#component)

**Returns** \
[Type](https://learn.microsoft.com/en-us/dotnet/api/System.Type?view=net-7.0) \

#### EditorName

```csharp
public string EditorName { get; }
```

The display name shown in the dialogue editor, equal to `Name`.

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### Kind

```csharp
public readonly FactKind Kind;
```

The data type of this fact's value (`Bool`, `Int`, `Float`, `String`, `Component`, etc.).

**Returns** \
[FactKind](../../../Murder/Core/Dialogs/FactKind.html) \

#### Name

```csharp
public readonly string Name;
```

The field name of the blackboard variable this fact refers to.

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

⚡
