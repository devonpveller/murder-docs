# NineSliceInfo

**Namespace:** Murder.Core.Graphics \
**Assembly:** Murder.dll

```csharp
public sealed struct NineSliceInfo
```

Defines a nine-slice sprite by referencing a `SpriteAsset` and the central stretchable rectangle within it.

**Intent:** Stores the asset GUID and core rectangle needed to render a nine-slice panel, decoupling the data definition from the cached geometry.

**Use-case:** Set on UI components (e.g., button backgrounds, dialog boxes) via the editor; call `Draw()` at runtime to render the panel stretched to any target size, or call `Cache()` for repeated draws without repeated asset lookups.

### ⭐ Constructors
```csharp
public NineSliceInfo()
```

Creates an empty `NineSliceInfo` with no asset or core rectangle.

```csharp
public NineSliceInfo(Rectangle core, Guid image)
```

**Parameters** \
`core` [Rectangle](../../../Murder/Core/Geometry/Rectangle.html) \
`image` [Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \

```csharp
public NineSliceInfo(Guid image)
```

**Parameters** \
`image` [Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \

### ⭐ Properties
#### Core
```csharp
public readonly Rectangle Core;
```

The central rectangle (in sprite-local pixels) that defines the stretchable region; outer slices are drawn un-stretched at the corners and edges.

**Returns** \
[Rectangle](../../../Murder/Core/Geometry/Rectangle.html) \
#### Empty
```csharp
public static NineSliceInfo Empty { get; }
```

A default-initialised `NineSliceInfo` with an empty GUID and no core rectangle; safe to use as a null-equivalent sentinel.

**Returns** \
[NineSliceInfo](../../../Murder/Core/Graphics/NineSliceInfo.html) \
#### Image
```csharp
public readonly Guid Image;
```

GUID of the `SpriteAsset` used as the source image for nine-slice rendering.

**Returns** \
[Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \
### ⭐ Methods
#### Cache()
```csharp
public CachedNineSlice Cache()
```

Resolves the asset GUID and returns a `CachedNineSlice` that holds a direct reference to the loaded `SpriteAsset`, avoiding repeated lookups on subsequent draws.

**Returns** \
[CachedNineSlice](../../../Murder/Core/Graphics/CachedNineSlice.html) \

#### Draw(Batch2D, Rectangle, DrawInfo, AnimationInfo)
```csharp
public void Draw(Batch2D batch, Rectangle target, DrawInfo info, AnimationInfo animationInfo)
```

Draws the nine-slice stretched to `target`, selecting the animation frame specified by `animationInfo`.

**Parameters** \
`batch` [Batch2D](../../../Murder/Core/Graphics/Batch2D.html) \
`target` [Rectangle](../../../Murder/Core/Geometry/Rectangle.html) \
`info` [DrawInfo](../../../Murder/Core/Graphics/DrawInfo.html) \
`animationInfo` [AnimationInfo](../../../Murder/Core/Graphics/AnimationInfo.html) \

#### Draw(Batch2D, Rectangle, string, Color, float)
```csharp
public void Draw(Batch2D batch, Rectangle target, string animation, Color color, float sort)
```

Draws the nine-slice stretched to `target` using the named `animation` clip and the given tint color and sort depth.

**Parameters** \
`batch` [Batch2D](../../../Murder/Core/Graphics/Batch2D.html) \
`target` [Rectangle](../../../Murder/Core/Geometry/Rectangle.html) \
`animation` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
`color` [Color](../../../Murder/Core/Graphics/Color.html) \
`sort` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \



⚡