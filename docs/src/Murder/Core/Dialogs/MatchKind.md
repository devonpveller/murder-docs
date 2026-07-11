# MatchKind

**Namespace:** Murder.Core.Dialogs \
**Assembly:** Murder.dll

```csharp
public sealed enum MatchKind : Enum, IComparable, ISpanFormattable, IFormattable, IConvertible
```

Defines the strategy used by a `DialogEdge` to select the next dialog node from a set of candidates.

**Intent:** Controls how the runtime picks which `Dialog` to visit next when multiple successors are listed on an edge — picking sequentially, randomly, by score, or presenting all as player choices.

**Use-case:** Set `DialogEdge.Kind` in the dialogue editor to determine how successor dialogs are ordered and chosen at runtime.

**Implements:** _[Enum](https://learn.microsoft.com/en-us/dotnet/api/System.Enum?view=net-7.0), [IComparable](https://learn.microsoft.com/en-us/dotnet/api/System.IComparable?view=net-7.0), [ISpanFormattable](https://learn.microsoft.com/en-us/dotnet/api/System.ISpanFormattable?view=net-7.0), [IFormattable](https://learn.microsoft.com/en-us/dotnet/api/System.IFormattable?view=net-7.0), [IConvertible](https://learn.microsoft.com/en-us/dotnet/api/System.IConvertible?view=net-7.0)_

### ⭐ Properties
#### Choice
```csharp
public static const MatchKind Choice;
```

Choice dialogs (&gt;) that the player can pick.

**Returns** \
[MatchKind](../../../Murder/Core/Dialogs/MatchKind.html) \
#### HighestScore
```csharp
public static const MatchKind HighestScore;
```

This will pick the dialog with the highest score.
            This is when dialogs are listed with -/+.

**Returns** \
[MatchKind](../../../Murder/Core/Dialogs/MatchKind.html) \
#### IfElse
```csharp
public static const MatchKind IfElse;
```

All the blocks that are next are subjected to an "else" relationship.

**Returns** \
[MatchKind](../../../Murder/Core/Dialogs/MatchKind.html) \
#### Next
```csharp
public static const MatchKind Next;
```

This will pick in consecutive order, whatever matches first.

**Returns** \
[MatchKind](../../../Murder/Core/Dialogs/MatchKind.html) \
#### Random
```csharp
public static const MatchKind Random;
```

This will pick random dialogs.

**Returns** \
[MatchKind](../../../Murder/Core/Dialogs/MatchKind.html) \


⚡