# CachedNineSlice

**Namespace:** Murder.Core.Graphics \
**Assembly:** Murder.dll

```csharp
public sealed struct CachedNineSlice
```

A pre-resolved nine-slice that holds a direct reference to the loaded `SpriteAsset` and its core rectangle, eliminating asset lookups on every draw call.

**Intent:** Caches the expensive `Game.Data.GetAsset<SpriteAsset>()` call so that nine-slice UI elements can be drawn each frame without incurring dictionary lookups.

**Use-case:** Call `NineSliceInfo.Cache()` once (e.g., at component initialization) and store the result; then call `CachedNineSlice.Draw()` every frame instead of drawing through `NineSliceInfo` directly.

### ⭐ Constructors
```csharp
public CachedNineSlice(NineSliceInfo info)
```

Creates a cached nine-slice from an existing `NineSliceInfo`, loading the sprite asset immediately.

**Parameters** \
`info` [NineSliceInfo](../../../Murder/Core/Graphics/NineSliceInfo.html) \

```csharp
public CachedNineSlice(Guid SpriteAsset)
```

Creates a cached nine-slice directly from a sprite asset GUID, using the asset's built-in nine-slice rectangle.

**Parameters** \
`SpriteAsset` [Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \

### ⭐ Properties
#### _core
```csharp
public readonly Rectangle _core;
```

The central rectangle (in sprite-local pixels) that defines the stretchable region of the nine-slice.

**Returns** \
[Rectangle](../../../Murder/Core/Geometry/Rectangle.html) \
#### _image
```csharp
public readonly SpriteAsset _image;
```

The pre-loaded sprite asset whose first animation frame is used as the nine-slice source image.

**Returns** \
[SpriteAsset](../../../Murder/Assets/Graphics/SpriteAsset.html) \
### ⭐ Methods
#### Draw(Batch2D, Rectangle, DrawInfo, AnimationInfo)
```csharp
public void Draw(Batch2D batch, Rectangle target, DrawInfo drawInfo, AnimationInfo animationInfo)
```

Draws the nine-slice stretched to `target`, using `animationInfo` to select the correct animation frame.

**Parameters** \
`batch` [Batch2D](../../../Murder/Core/Graphics/Batch2D.html) \
`target` [Rectangle](../../../Murder/Core/Geometry/Rectangle.html) \
`drawInfo` [DrawInfo](../../../Murder/Core/Graphics/DrawInfo.html) \
`animationInfo` [AnimationInfo](../../../Murder/Core/Graphics/AnimationInfo.html) \

#### Draw(Batch2D, Rectangle, DrawInfo)
```csharp
public void Draw(Batch2D batch, Rectangle target, DrawInfo drawInfo)
```

Draws the nine-slice stretched to `target` using the default animation frame.

**Parameters** \
`batch` [Batch2D](../../../Murder/Core/Graphics/Batch2D.html) \
`target` [Rectangle](../../../Murder/Core/Geometry/Rectangle.html) \
`drawInfo` [DrawInfo](../../../Murder/Core/Graphics/DrawInfo.html) \

#### DrawWithText(Batch2D, string, int, Color, T?, T?, Rectangle, float)
```csharp
public void DrawWithText(Batch2D batch, string text, int font, Color textColor, T? textOutlineColor, T? textShadowColor, Rectangle target, float sort)
```

Draws the nine-slice background and overlays centered `text` on top of it in one call; convenient for labeled buttons and panels.

**Parameters** \
`batch` [Batch2D](../../../Murder/Core/Graphics/Batch2D.html) \
`text` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
`font` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`textColor` [Color](../../../Murder/Core/Graphics/Color.html) \
`textOutlineColor` [T?](https://learn.microsoft.com/en-us/dotnet/api/System.Nullable-1?view=net-7.0) \
`textShadowColor` [T?](https://learn.microsoft.com/en-us/dotnet/api/System.Nullable-1?view=net-7.0) \
`target` [Rectangle](../../../Murder/Core/Geometry/Rectangle.html) \
`sort` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \



⚡