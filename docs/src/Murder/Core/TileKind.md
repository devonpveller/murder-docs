# TileKind

**Namespace:** Murder.Core \
**Assembly:** Murder.dll

```csharp
public sealed enum TileKind : Enum, IComparable, ISpanFormattable, IFormattable, IConvertible
```

Distinguishes the two primary roles a tile layer can serve: physics collision or trigger detection.

**Intent:** A two-value discriminator that tells the map-building system whether a tilemap entity contributes to the solid collision layer or to the trigger layer.

**Use-case:** Set on a tilemap component so systems that populate the `Map` know which collision layer to apply when rasterizing the tile data.

**Implements:** _[Enum](https://learn.microsoft.com/en-us/dotnet/api/System.Enum?view=net-7.0), [IComparable](https://learn.microsoft.com/en-us/dotnet/api/System.IComparable?view=net-7.0), [ISpanFormattable](https://learn.microsoft.com/en-us/dotnet/api/System.ISpanFormattable?view=net-7.0), [IFormattable](https://learn.microsoft.com/en-us/dotnet/api/System.IFormattable?view=net-7.0), [IConvertible](https://learn.microsoft.com/en-us/dotnet/api/System.IConvertible?view=net-7.0)_

### ⭐ Properties
#### Physics
```csharp
public static const TileKind Physics;
```

This tile layer provides solid physics collision that blocks movement.

**Returns** \
[TileKind](../../Murder/Core/TileKind.html) \
#### Trigger
```csharp
public static const TileKind Trigger;
```

This tile layer marks areas that fire trigger interactions when an actor enters them.

**Returns** \
[TileKind](../../Murder/Core/TileKind.html) \


⚡