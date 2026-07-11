# NineSliceStyle

**Namespace:** Murder.Core.Graphics \
**Assembly:** Murder.dll

```csharp
public sealed enum NineSliceStyle : Enum, IComparable, ISpanFormattable, IFormattable, IConvertible
```

**Implements:** _[Enum](https://learn.microsoft.com/en-us/dotnet/api/System.Enum?view=net-7.0), [IComparable](https://learn.microsoft.com/en-us/dotnet/api/System.IComparable?view=net-7.0), [ISpanFormattable](https://learn.microsoft.com/en-us/dotnet/api/System.ISpanFormattable?view=net-7.0), [IFormattable](https://learn.microsoft.com/en-us/dotnet/api/System.IFormattable?view=net-7.0), [IConvertible](https://learn.microsoft.com/en-us/dotnet/api/System.IConvertible?view=net-7.0)_

Controls how the center and edge regions of a 9-slice sprite are rendered when its container is scaled.

**Intent:** Determines whether the interior tiles of a 9-slice image are stretched or tiled to fill the target rectangle.

**Use-case:** Assign to `NineSliceInfo` or `CachedNineSlice` to choose between a smooth stretched panel (`Stretch`) and a repeating tile pattern (`Tile`) when drawing resizable UI frames.

### ⭐ Properties
#### Stretch
```csharp
public static const NineSliceStyle Stretch;
```

Stretches all center and edge tiles uniformly to fill the target rectangle.

**Returns** \
[NineSliceStyle](../../../Murder/Core/Graphics/NineSliceStyle.html) \
#### Tile
```csharp
public static const NineSliceStyle Tile;
```

Repeats (tiles) the center and edge pieces instead of stretching them, preserving their original pixel size.

**Returns** \
[NineSliceStyle](../../../Murder/Core/Graphics/NineSliceStyle.html) \


⚡