# AlphaSources

**Namespace:** Murder.Components \
**Assembly:** Murder.dll

```csharp
public sealed enum AlphaSources : Enum, IComparable, ISpanFormattable, IFormattable, IConvertible
```

Identifies the independent slots that contribute to an entity's final alpha value in `AlphaComponent`.

**Implements:** _[Enum](https://learn.microsoft.com/en-us/dotnet/api/System.Enum?view=net-7.0), [IComparable](https://learn.microsoft.com/en-us/dotnet/api/System.IComparable?view=net-7.0), [ISpanFormattable](https://learn.microsoft.com/en-us/dotnet/api/System.ISpanFormattable?view=net-7.0), [IFormattable](https://learn.microsoft.com/en-us/dotnet/api/System.IFormattable?view=net-7.0), [IConvertible](https://learn.microsoft.com/en-us/dotnet/api/System.IConvertible?view=net-7.0)_

**Intent:** Lets multiple systems each own a dedicated alpha channel without interfering with each other.

**Use-case:** Use `AlphaSources.Fade` in a fade system and `AlphaSources.Alpha` in game logic; the final on-screen transparency is the product of both slots.

### ⭐ Properties
#### Alpha
```csharp
public static const AlphaSources Alpha;
```

General-purpose alpha slot, typically driven by game-logic or script systems.

**Returns** \
[AlphaSources](../../Murder/Components/AlphaSources.html) \
#### Fade
```csharp
public static const AlphaSources Fade;
```

Alpha slot reserved for fade-in/fade-out transition effects.

**Returns** \
[AlphaSources](../../Murder/Components/AlphaSources.html) \
#### LastSeen
```csharp
public static const AlphaSources LastSeen;
```

Alpha slot used to dim an entity that was recently visible but is now out of sight (e.g., fog-of-war silhouette).

**Returns** \
[AlphaSources](../../Murder/Components/AlphaSources.html) \


⚡