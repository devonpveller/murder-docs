# Criterion

**Namespace:** Murder.Core.Dialogs \
**Assembly:** Murder.dll

```csharp
public sealed struct Criterion
```

Represents a single condition that compares a blackboard `Fact` to a literal value using a `CriterionKind` operator.

**Intent:** Encapsulates one conditional test — a fact reference, a comparison operator, and the expected value — used to guard `Dialog` nodes so they only play when their conditions are met.

**Use-case:** Build criteria in the dialogue editor or in code and group them into `CriterionNode` lists on a `Dialog`; the engine evaluates them against live blackboard data via `CharacterRuntime.CheckRequirements`.

### ⭐ Constructors

```csharp
public Criterion()
```

Creates an empty criterion with default values (`FactKind.Invalid`, `CriterionKind.Is`).

```csharp
public Criterion(Fact fact, CriterionKind kind, Object value)
```

Creates a criterion comparing `fact` with `kind` against a boxed `value`; the value is stored in the typed slot matching the fact's `FactKind`.

**Parameters** \
`fact` [Fact](../../../Murder/Core/Dialogs/Fact.html) \
`kind` [CriterionKind](../../../Murder/Core/Dialogs/CriterionKind.html) \
`value` [Object](https://learn.microsoft.com/en-us/dotnet/api/System.Object?view=net-7.0) \

```csharp
public Criterion(Fact fact, CriterionKind kind, T? bool, T? int, T? float, string string)
```

Creates a criterion with all typed value slots supplied explicitly; prefer the `Criterion(Fact, CriterionKind, Object)` overload when the value is a single boxed object, and use this overload when the value is already decomposed.

**Parameters** \
`fact` [Fact](../../../Murder/Core/Dialogs/Fact.html) \
`kind` [CriterionKind](../../../Murder/Core/Dialogs/CriterionKind.html) \
`bool` [T?](https://learn.microsoft.com/en-us/dotnet/api/System.Nullable-1?view=net-7.0) \
`int` [T?](https://learn.microsoft.com/en-us/dotnet/api/System.Nullable-1?view=net-7.0) \
`float` [T?](https://learn.microsoft.com/en-us/dotnet/api/System.Nullable-1?view=net-7.0) \
`string` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
`value` [Object](https://learn.microsoft.com/en-us/dotnet/api/System.Object?view=net-7.0) \

### ⭐ Properties

#### BoolValue

```csharp
public readonly T? BoolValue;
```

The boolean comparison value; populated when the fact is of kind `Bool`.

**Returns** \
[T?](https://learn.microsoft.com/en-us/dotnet/api/System.Nullable-1?view=net-7.0) \

#### Component

```csharp
public static Criterion Component { get; }
```

Creates a criterion of type [FactKind.Component](../../../Murder/Core/Dialogs/FactKind.html#component), used to require (or, combined with `CriterionKind.Different`, forbid) that the target entity currently holds a specific component.

**Returns** \
[Criterion](../../../Murder/Core/Dialogs/Criterion.html) \

#### Fact

```csharp
public readonly Fact Fact;
```

The blackboard variable being tested by this criterion.

**Returns** \
[Fact](../../../Murder/Core/Dialogs/Fact.html) \

#### FloatValue

```csharp
public readonly T? FloatValue;
```

The float comparison value; populated when the fact is of kind `Float`.

**Returns** \
[T?](https://learn.microsoft.com/en-us/dotnet/api/System.Nullable-1?view=net-7.0) \

#### IntValue

```csharp
public readonly T? IntValue;
```

The integer comparison value; populated when the fact is of kind `Int` or `Weight`.

**Returns** \
[T?](https://learn.microsoft.com/en-us/dotnet/api/System.Nullable-1?view=net-7.0) \

#### Kind

```csharp
public readonly CriterionKind Kind;
```

The comparison operator applied between the fact's live value and the stored literal value.

**Returns** \
[CriterionKind](../../../Murder/Core/Dialogs/CriterionKind.html) \

#### StrValue

```csharp
public readonly string StrValue;
```

The string comparison value; populated when the fact is of kind `String`.

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### Weight

```csharp
public static Criterion Weight { get; }
```

Creates a criterion of type [FactKind.Weight](../../../Murder/Core/Dialogs/FactKind.html#weight) with an integer value of 1, used to add a flat score bonus to a dialog when it is chosen via `MatchKind.HighestScore`.

**Returns** \
[Criterion](../../../Murder/Core/Dialogs/Criterion.html) \

⚡
