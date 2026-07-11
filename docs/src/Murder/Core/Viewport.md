# Viewport

**Namespace:** Murder.Core \
**Assembly:** Murder.dll

```csharp
public sealed struct Viewport
```

Describes the camera viewport: the game's native resolution, the actual window size, the scale factor applied, and the output rectangle on screen.

**Intent:** Immutable snapshot of how the game's render output maps onto the display window, accounting for letterboxing and scaling.

**Use-case:** Queried by the render context and camera systems to determine where to draw the game's output rectangle and how to map screen-space coordinates to world space.

### ⭐ Constructors
```csharp
public Viewport(Point viewportSize, Point nativeResolution, ViewportResizeStyle resizeStyle)
```

Creates a viewport that maps `nativeResolution` onto a window of `viewportSize` using the specified resize style.

**Parameters** \
`viewportSize` [Point](../../Murder/Core/Geometry/Point.html) \
`nativeResolution` [Point](../../Murder/Core/Geometry/Point.html) \
`resizeStyle` [ViewportResizeStyle](../../Murder/Core/Graphics/ViewportResizeStyle.html) \

### ⭐ Properties
#### Center
```csharp
public readonly Vector2 Center;
```

The center of the output rectangle in screen-space pixels.

**Returns** \
[Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
#### NativeResolution
```csharp
public readonly Point NativeResolution;
```

The resolution that the game is actually rendered

**Returns** \
[Point](../../Murder/Core/Geometry/Point.html) \
#### OutputRectangle
```csharp
public readonly IntRectangle OutputRectangle;
```

The rectangle where the game should be rendered on the screen.

**Returns** \
[IntRectangle](../../Murder/Core/Geometry/IntRectangle.html) \
#### Scale
```csharp
public readonly Vector2 Scale;
```

The scale that is applied to the native resolution before rendering

**Returns** \
[Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
#### Size
```csharp
public readonly Point Size;
```

The size of the viewport (tipically the game's window)

**Returns** \
[Point](../../Murder/Core/Geometry/Point.html) \
### ⭐ Methods
#### HasChanges(Point, Vector2)
```csharp
public bool HasChanges(Point size, Vector2 scale)
```

Returns `true` when `size` or `scale` differ from the current viewport values, indicating the viewport needs to be rebuilt.

**Parameters** \
`size` [Point](../../Murder/Core/Geometry/Point.html) \
`scale` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \



⚡