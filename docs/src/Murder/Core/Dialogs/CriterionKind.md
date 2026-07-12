# CriterionKind

**Namespace:** Murder.Core.Dialogs \
**Assembly:** Murder.dll

```csharp
public sealed enum CriterionKind : Enum, IComparable, ISpanFormattable, IFormattable, IConvertible
```

Specifies the comparison operator used in a `Criterion` to test a blackboard fact against a value.

**Intent:** Enumerates the full set of relational operators — equality, inequality, and numeric ordering — that can be applied when evaluating dialogue conditions.

**Use-case:** Set `Criterion.Kind` to the desired operator when authoring dialogue conditions; at runtime the engine compares the live fact value to the criterion's stored value using this operator.

**Implements:** _[Enum](https://learn.microsoft.com/en-us/dotnet/api/System.Enum?view=net-7.0), [IComparable](https://learn.microsoft.com/en-us/dotnet/api/System.IComparable?view=net-7.0), [ISpanFormattable](https://learn.microsoft.com/en-us/dotnet/api/System.ISpanFormattable?view=net-7.0), [IFormattable](https://learn.microsoft.com/en-us/dotnet/api/System.IFormattable?view=net-7.0), [IConvertible](https://learn.microsoft.com/en-us/dotnet/api/System.IConvertible?view=net-7.0)_

### ⭐ Properties

#### Bigger

```csharp
public static const CriterionKind Bigger;
```

Passes when the fact's value is strictly greater than the criterion value (`fact > value`).

**Returns** \
[CriterionKind](../../../Murder/Core/Dialogs/CriterionKind.html) \

#### BiggerOrEqual

```csharp
public static const CriterionKind BiggerOrEqual;
```

Passes when the fact's value is greater than or equal to the criterion value (`fact >= value`).

**Returns** \
[CriterionKind](../../../Murder/Core/Dialogs/CriterionKind.html) \

#### Different

```csharp
public static const CriterionKind Different;
```

Passes when the fact's value does not equal the criterion value (`fact != value`).

**Returns** \
[CriterionKind](../../../Murder/Core/Dialogs/CriterionKind.html) \

#### Is

```csharp
public static const CriterionKind Is;
```

Passes when the fact's value equals the criterion value (`fact == value`).

**Returns** \
[CriterionKind](../../../Murder/Core/Dialogs/CriterionKind.html) \

#### Less

```csharp
public static const CriterionKind Less;
```

Passes when the fact's value is strictly less than the criterion value (`fact < value`).

**Returns** \
[CriterionKind](../../../Murder/Core/Dialogs/CriterionKind.html) \

#### LessOrEqual

```csharp
public static const CriterionKind LessOrEqual;
```

Passes when the fact's value is less than or equal to the criterion value (`fact <= value`).

**Returns** \
[CriterionKind](../../../Murder/Core/Dialogs/CriterionKind.html) \

⚡
