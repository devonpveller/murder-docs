# DialogLine

**Namespace:** Murder.Core.Dialogs \
**Assembly:** Murder.dll

```csharp
public sealed struct DialogLine
```

A discriminated union returned by `CharacterRuntime.NextLine` that holds either a regular `Line` or a `ChoiceLine`.

**Intent:** Provides a single return type for `NextLine` that covers both normal narrative lines and player-choice prompts without requiring an interface or base class.

**Use-case:** Check `Line` or `Choice` for `null` to determine which variant was returned, then render accordingly and call `DoChoice` if a `ChoiceLine` was received.

### ⭐ Constructors
```csharp
public DialogLine(ChoiceLine choice)
```

Creates a `DialogLine` wrapping a choice prompt; `Line` will be `null`.

**Parameters** \
`choice` [ChoiceLine](../../../Murder/Core/Dialogs/ChoiceLine.html) \

```csharp
public DialogLine(Line line)
```

Creates a `DialogLine` wrapping a narrative line; `Choice` will be `null`.

**Parameters** \
`line` [Line](../../../Murder/Core/Dialogs/Line.html) \

### ⭐ Properties
#### Choice
```csharp
public readonly T? Choice;
```

The choice prompt to present to the player, or `null` when this line is a plain narrative `Line`.

**Returns** \
[T?](https://learn.microsoft.com/en-us/dotnet/api/System.Nullable-1?view=net-7.0) \
#### Line
```csharp
public readonly T? Line;
```

The narrative line to display, or `null` when this line is a `ChoiceLine`.

**Returns** \
[T?](https://learn.microsoft.com/en-us/dotnet/api/System.Nullable-1?view=net-7.0) \


⚡