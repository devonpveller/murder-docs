# FactKind

**Namespace:** Murder.Core.Dialogs \
**Assembly:** Murder.dll

```csharp
public sealed enum FactKind : Enum, IComparable, ISpanFormattable, IFormattable, IConvertible
```

Specifies the data type of a blackboard `Fact` variable.

**Intent:** Tells the dialogue system and editor which storage slot and comparison logic to use when reading or writing a `Fact`.

**Use-case:** Set `Fact.Kind` when creating a `Fact`; the engine uses this to know how to serialize, display, compare, and mutate the variable's value.

**Implements:** _[Enum](https://learn.microsoft.com/en-us/dotnet/api/System.Enum?view=net-7.0), [IComparable](https://learn.microsoft.com/en-us/dotnet/api/System.IComparable?view=net-7.0), [ISpanFormattable](https://learn.microsoft.com/en-us/dotnet/api/System.ISpanFormattable?view=net-7.0), [IFormattable](https://learn.microsoft.com/en-us/dotnet/api/System.IFormattable?view=net-7.0), [IConvertible](https://learn.microsoft.com/en-us/dotnet/api/System.IConvertible?view=net-7.0)_

### ⭐ Properties

#### Any

```csharp
public static const FactKind Any;
```

Matches a fact of any data type; used for broad queries that are not type-specific.

**Returns** \
[FactKind](../../../Murder/Core/Dialogs/FactKind.html) \

#### Bool

```csharp
public static const FactKind Bool;
```

The fact stores a boolean value (`true` / `false`).

**Returns** \
[FactKind](../../../Murder/Core/Dialogs/FactKind.html) \

#### Component

```csharp
public static const FactKind Component;
```

Used when checking for required components.

**Returns** \
[FactKind](../../../Murder/Core/Dialogs/FactKind.html) \

#### Enum

```csharp
public static const FactKind Enum;
```

The fact stores an enumeration value.

**Returns** \
[FactKind](../../../Murder/Core/Dialogs/FactKind.html) \

#### Float

```csharp
public static const FactKind Float;
```

The fact stores a single-precision floating-point value.

**Returns** \
[FactKind](../../../Murder/Core/Dialogs/FactKind.html) \

#### Int

```csharp
public static const FactKind Int;
```

The fact stores an integer value.

**Returns** \
[FactKind](../../../Murder/Core/Dialogs/FactKind.html) \

#### Invalid

```csharp
public static const FactKind Invalid;
```

Default sentinel value indicating an uninitialized or erroneous fact; should not appear in authored data.

**Returns** \
[FactKind](../../../Murder/Core/Dialogs/FactKind.html) \

#### String

```csharp
public static const FactKind String;
```

The fact stores a text string value.

**Returns** \
[FactKind](../../../Murder/Core/Dialogs/FactKind.html) \

#### Weight

```csharp
public static const FactKind Weight;
```

Used when the fact is only a weight which will be applied when picking
the most suitable dialog.

**Returns** \
[FactKind](../../../Murder/Core/Dialogs/FactKind.html) \

⚡
