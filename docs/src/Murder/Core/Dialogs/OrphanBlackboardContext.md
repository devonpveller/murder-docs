# OrphanBlackboardContext

**Namespace:** Murder.Core.Dialogs \
**Assembly:** Murder.dll

```csharp
public sealed struct OrphanBlackboardContext
```

This is used to track variables created on the fly. This used to be an
object, but the serialization doesn't really like that, so I'll follow a
similar pattern to other facts.

**Intent:** Provides a serialization-friendly tagged union that stores a single runtime blackboard value (of any `FactKind`) without being tied to a named `IBlackboard` field.

**Use-case:** Used internally by the engine to persist ad-hoc blackboard values that do not belong to a specific blackboard class — for example, when a world or save-level fact is created dynamically.

### ⭐ Constructors

```csharp
public OrphanBlackboardContext()
```

Creates an empty context with `FactKind.Invalid`.

```csharp
public OrphanBlackboardContext(FactKind kind, T? boolValue, T? intValue, T? floatValue, string strValue)
```

Creates a context with explicit kind and typed value slots; used for JSON deserialization.

**Parameters** \
`kind` [FactKind](../../../Murder/Core/Dialogs/FactKind.html) \
`boolValue` [T?](https://learn.microsoft.com/en-us/dotnet/api/System.Nullable-1?view=net-7.0) \
`intValue` [T?](https://learn.microsoft.com/en-us/dotnet/api/System.Nullable-1?view=net-7.0) \
`floatValue` [T?](https://learn.microsoft.com/en-us/dotnet/api/System.Nullable-1?view=net-7.0) \
`strValue` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

```csharp
public OrphanBlackboardContext(Object value)
```

Creates a context by inspecting the runtime type of `value` to infer the `FactKind` and populate the correct slot.

**Parameters** \
`value` [Object](https://learn.microsoft.com/en-us/dotnet/api/System.Object?view=net-7.0) \

### ⭐ Properties

#### BoolValue

```csharp
public readonly T? BoolValue;
```

The stored boolean value; non-null when `Kind` is `Bool`.

**Returns** \
[T?](https://learn.microsoft.com/en-us/dotnet/api/System.Nullable-1?view=net-7.0) \

#### FloatValue

```csharp
public readonly T? FloatValue;
```

The stored float value; non-null when `Kind` is `Float`.

**Returns** \
[T?](https://learn.microsoft.com/en-us/dotnet/api/System.Nullable-1?view=net-7.0) \

#### IntValue

```csharp
public readonly T? IntValue;
```

The stored integer value; non-null when `Kind` is `Int`.

**Returns** \
[T?](https://learn.microsoft.com/en-us/dotnet/api/System.Nullable-1?view=net-7.0) \

#### Kind

```csharp
public readonly FactKind Kind;
```

The data type of the stored value, indicating which slot (`BoolValue`, `IntValue`, etc.) is populated.

**Returns** \
[FactKind](../../../Murder/Core/Dialogs/FactKind.html) \

#### StrValue

```csharp
public readonly string StrValue;
```

The stored string value; non-null when `Kind` is `String`.

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

### ⭐ Methods

#### GetValue()

```csharp
public Object GetValue()
```

Returns the stored value as a boxed `object` based on the current `Kind`.

**Returns** \
[Object](https://learn.microsoft.com/en-us/dotnet/api/System.Object?view=net-7.0) \

⚡
