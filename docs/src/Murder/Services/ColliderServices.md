# ColliderServices

**Namespace:** Murder.Services \
**Assembly:** Murder.dll

```csharp
public static class ColliderServices
```

Helpers for computing bounding boxes, grid snapping, and center points from an entity's `ColliderComponent`.

**Intent:** Provides geometry utilities that operate directly on entities carrying `PositionComponent`/`ColliderComponent`, so callers don't need to manually fetch those components and repeat the bounding-box/scale math themselves.

**Use-case:** Use to determine where an entity sits in world or grid space — for example when placing objects on a tile grid (`SnapToGrid`, `ToGrid`), centering a UI element or highlight over an entity (`FindCenter`, `GetCenterOf`), or feeding collider shapes into other systems (`GetCollidersBoundingBox`, `GetBoundingBox`).

### ⭐ Methods

#### FindCenter(Entity)

```csharp
public static Point FindCenter(Entity e)
```

Returns the center point of the entity's combined collider bounding box (`GetBoundingBox(e).CenterPoint`). Useful for centering UI, VFX, or camera framing on an entity's collision volume rather than its raw position, since colliders can be offset from the entity's origin.

**Parameters** \
`e` [Entity](../../Bang/Entities/Entity.html) \

**Returns** \
[Point](../../Murder/Core/Geometry/Point.html) \

#### GetBoundingBox(Entity)

```csharp
public static IntRectangle GetBoundingBox(Entity e)
```

Returns the integer bounding rectangle of the entity's collider in world coordinates, accounting for the entity's global position and scale. Returns `IntRectangle.Empty` if the entity has no `ColliderComponent`.

**Parameters** \
`e` [Entity](../../Bang/Entities/Entity.html) \

**Returns** \
[IntRectangle](../../Murder/Core/Geometry/IntRectangle.html) \

#### SnapToGrid(Vector2)

```csharp
public static Vector2 SnapToGrid(Vector2 positive)
```

Snaps a world-space position down to the origin of the grid cell it falls in, using `Grid.CellSize`. Intended for non-negative coordinates (per the parameter name); use `SnapToRelativeGrid` when snapping around an arbitrary origin, including negative offsets.

**Parameters** \
`positive` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

**Returns** \
[Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

#### SnapToRelativeGrid(Vector2, Vector2)

```csharp
public static Vector2 SnapToRelativeGrid(Vector2 position, Vector2 origin)
```

Snaps `position` to the nearest grid cell measured relative to `origin`, then translates the result back into world space by re-adding `origin`. Use this when the grid you're snapping to isn't anchored at world (0, 0) — for example a grid local to a room or object.

**Parameters** \
`position` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`origin` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

**Returns** \
[Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

#### ToGrid(IntRectangle)

```csharp
public static IntRectangle ToGrid(this IntRectangle rectangle)
```

Extension method that converts a pixel-space rectangle into grid-cell coordinates, flooring the top-left corner and ceiling the bottom-right corner (via `Grid.CellSize`) so the resulting rectangle fully covers every grid cell the original rectangle touches.

**Parameters** \
`rectangle` [IntRectangle](../../Murder/Core/Geometry/IntRectangle.html) \

**Returns** \
[IntRectangle](../../Murder/Core/Geometry/IntRectangle.html) \

#### GetCollidersBoundingBox(Entity, bool)

```csharp
public static IntRectangle[] GetCollidersBoundingBox(Entity e, bool gridCoordinates)
```

Returns one bounding box per shape in the entity's collider (delegating to `PhysicsServices.GetCollidersBoundingBox`), optionally converted to grid-cell coordinates instead of pixel coordinates. Use this over `GetBoundingBox` when you need per-shape granularity — e.g. carving individual solid tiles or evaluating multi-shape colliders separately — rather than a single combined box.

**Parameters** \
`e` [Entity](../../Bang/Entities/Entity.html) \
`gridCoordinates` [bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

**Returns** \
[IntRectangle[]](../../Murder/Core/Geometry/IntRectangle.html) \

#### GetCenterOf(Entity)

```csharp
public static Vector2 GetCenterOf(Entity e)
```

Returns the world-space center of the entity's collider bounding box as a `Vector2` (unlike `FindCenter`, which returns an integer `Point`). If the entity has no collider, this simply returns its global position. Prefer this over `FindCenter` when you need sub-pixel precision, e.g. for smooth camera targeting or physics calculations.

**Parameters** \
`e` [Entity](../../Bang/Entities/Entity.html) \

**Returns** \
[Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

⚡
