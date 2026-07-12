# TileKind

**Namespace:** Murder.Core \
**Assembly:** Murder.dll

```csharp
public sealed enum TileKind : Enum, IComparable, ISpanFormattable, IFormattable, IConvertible
```

Distinguishes the two roles a tile layer identifier can represent: solid physics collision or a trigger area.

**Intent:** A minimal, standalone two-value discriminator for code that wants a simple physics-vs-trigger categorization without depending on the full collision layer set.

**Use-case:** Note that the engine's actual tile/grid collision system (`Map`) is built on `CollisionLayersBase` bit flags (e.g. `SOLID`, `BLOCK_VISION`, `HOLE`), not on `TileKind` — this enum is not currently referenced anywhere else in the engine. Treat it as a lightweight vocabulary available to game-specific code rather than a type wired into `Map`/tilemap rendering.

**Implements:** _[Enum](https://learn.microsoft.com/en-us/dotnet/api/System.Enum?view=net-7.0), [IComparable](https://learn.microsoft.com/en-us/dotnet/api/System.IComparable?view=net-7.0), [ISpanFormattable](https://learn.microsoft.com/en-us/dotnet/api/System.ISpanFormattable?view=net-7.0), [IFormattable](https://learn.microsoft.com/en-us/dotnet/api/System.IFormattable?view=net-7.0), [IConvertible](https://learn.microsoft.com/en-us/dotnet/api/System.IConvertible?view=net-7.0)_

### ⭐ Properties

#### Physics

```csharp
public static const TileKind Physics;
```

Identifies a tile layer intended to represent solid physics collision.

**Returns** \
[TileKind](../../Murder/Core/TileKind.html) \

#### Trigger

```csharp
public static const TileKind Trigger;
```

Identifies a tile layer intended to represent a trigger area.

**Returns** \
[TileKind](../../Murder/Core/TileKind.html) \

⚡
