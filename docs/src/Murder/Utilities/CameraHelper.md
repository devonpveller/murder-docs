# CameraHelper

**Namespace:** Murder.Utilities \
**Assembly:** Murder.dll

```csharp
public static class CameraHelper
```

Extension methods on `Camera2D` for computing safe tile-grid cell bounds visible within the camera viewport.

**Intent:** Provides helpers that translate a 2D camera frustum into grid-cell coordinate ranges suitable for tile-map culling.

**Use-case:** Call `GetSafeGridBounds` from tile-map rendering systems to determine which cells are in view and should be drawn.

### ⭐ Methods
#### GetSafeGridBounds(Camera2D, Rectangle, int)
```csharp
public ValueTuple<T1, T2, T3, T4> GetSafeGridBounds(Camera2D camera, Rectangle rect, int extraPadding)
```

Returns the (minX, maxX, minY, maxY) grid cell range visible to the camera, clamped to `rect` and expanded by `extraPadding` cells.

**Parameters** \
`camera` [Camera2D](../../Murder/Core/Graphics/Camera2D.html) \
`rect` [Rectangle](https://docs.monogame.net/api/Microsoft.Xna.Framework.Rectangle.html) \
`extraPadding` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

**Returns** \
[ValueTuple\<T1, T2, T3, T4\>](https://learn.microsoft.com/en-us/dotnet/api/System.ValueTuple-4?view=net-7.0) \

#### GetSafeGridBounds(Camera2D, Map)
```csharp
public ValueTuple<T1, T2, T3, T4> GetSafeGridBounds(Camera2D camera, Map map)
```

Returns the (minX, maxX, minY, maxY) grid cell range visible to the camera, clamped to the map's dimensions.

**Parameters** \
`camera` [Camera2D](../../Murder/Core/Graphics/Camera2D.html) \
`map` [Map](../../Murder/Core/Map.html) \

**Returns** \
[ValueTuple\<T1, T2, T3, T4\>](https://learn.microsoft.com/en-us/dotnet/api/System.ValueTuple-4?view=net-7.0) \



⚡