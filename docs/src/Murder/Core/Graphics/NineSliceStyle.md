# NineSliceStyle

**Namespace:** Murder.Core.Graphics \
**Assembly:** Murder.dll

```csharp
public sealed enum NineSliceStyle : Enum, IComparable, ISpanFormattable, IFormattable, IConvertible
```

**Implements:** _[Enum](https://learn.microsoft.com/en-us/dotnet/api/System.Enum?view=net-7.0), [IComparable](https://learn.microsoft.com/en-us/dotnet/api/System.IComparable?view=net-7.0), [ISpanFormattable](https://learn.microsoft.com/en-us/dotnet/api/System.ISpanFormattable?view=net-7.0), [IFormattable](https://learn.microsoft.com/en-us/dotnet/api/System.IFormattable?view=net-7.0), [IConvertible](https://learn.microsoft.com/en-us/dotnet/api/System.IConvertible?view=net-7.0)_

Controls how the corner, edge and center regions of a 9-slice sprite are rendered when its target rectangle is larger than the source image.

**Intent:** Determines whether the interior tiles of a 9-slice image are stretched or tiled to fill the target rectangle, and whether the center tile is drawn at all.

**Use-case:** Assign to `NineSliceComponent.Style` (or pass directly to `RenderServices.Draw9Slice`) to choose between a smooth stretched panel (`Stretch`), a repeating tile pattern (`Tile`), or one of the "hollow" variants (`TileHollow`, `StrechHollow`) that skip the center tile entirely — useful when drawing just a border/frame around content that is rendered separately. Note that `NineSliceInfo` and `CachedNineSlice`'s own `Draw` overloads always draw with `Stretch`; use `RenderServices.Draw9Slice` directly to pick a different style.

### ⭐ Properties

#### Stretch

```csharp
public static const NineSliceStyle Stretch;
```

Stretches the center and edge regions uniformly to fill the target rectangle, keeping the corners undistorted. This is the default used by `NineSliceComponent` and by `NineSliceInfo`/`CachedNineSlice`'s `Draw` overloads.

**Returns** \
[NineSliceStyle](../../../Murder/Core/Graphics/NineSliceStyle.html) \

#### Tile

```csharp
public static const NineSliceStyle Tile;
```

Repeats (tiles) the center and edge pieces at their original pixel size instead of stretching them, so patterns (e.g. brick or dot textures) don't distort when the panel is resized.

**Returns** \
[NineSliceStyle](../../../Murder/Core/Graphics/NineSliceStyle.html) \

#### TileHollow

```csharp
public static const NineSliceStyle TileHollow;
```

Same as `Tile`, but the center region is skipped entirely, leaving the middle of the panel transparent.

**Returns** \
[NineSliceStyle](../../../Murder/Core/Graphics/NineSliceStyle.html) \

#### StrechHollow

```csharp
public static const NineSliceStyle StrechHollow;
```

Same as `Stretch`, but the center region is skipped entirely, leaving the middle of the panel transparent. Note the spelling (`Strech`, not `Stretch`) matches the enum member name as declared in the engine source.

**Returns** \
[NineSliceStyle](../../../Murder/Core/Graphics/NineSliceStyle.html) \

⚡
