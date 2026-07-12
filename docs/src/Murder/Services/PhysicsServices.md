# PhysicsServices

**Namespace:** Murder.Services \
**Assembly:** Murder.dll

```csharp
public static class PhysicsServices
```

Provides collision detection, raycasting, overlap/MTV queries, and spatial-search utility methods for the Murder ECS world.

**Intent:** Centralises all physics and spatial-query operations — tile collision, entity-vs-entity collision, raycasting against both tiles and entities, and minimum-translation-vector (MTV) resolution — so game systems can test collisions and find entities in the world without manually iterating components or the quadtree themselves. Also declares two nested helper types used throughout its own API: `RaycastHit` (the result of a raycast) and `PhysicEntityCachedInfo` (a lightweight, pre-fetched snapshot of an entity's id/scale/position/collider, used to avoid repeated component lookups across a batch of collision checks), plus the nested `NextAvailablePositionFlags` enum consumed by `FindNextAvailablePosition`.

**Use-case:** Use `Raycast`/`RaycastTiles` for projectile line-of-sight and hit-scan checks, `HasLineOfSight`/`CanSeeEntity` for AI vision checks, `CollidesWith`/`CollidesAt`/`GetAllCollisionsAt` for overlap detection, the `FilterPositionAndColliderEntities` family to gather candidate entities by collision layer before running your own checks against them, and `FindNextAvailablePosition` to safely place or push an entity without overlapping obstacles.

### ⭐ Methods

#### AddToCollisionCache(Entity, int)

```csharp
public static void AddToCollisionCache(Entity entity, int entityId)
```

Adds `entityId` to `entity`'s `CollisionCacheComponent` (creating the component if it doesn't exist yet), marking that the two are currently considered to be colliding. Used by trigger/collision systems to remember which entities are currently overlapping so enter/exit events can be raised correctly.

**Parameters** \
`entity` [Entity](../../Bang/Entities/Entity.html) \
`entityId` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### AddVelocity(Entity, Vector2)

```csharp
public static void AddVelocity(this Entity entity, Vector2 addVelocity)
```

Adds `addVelocity` to the entity's current `VelocityComponent` (treating a missing component as zero velocity), replacing it with the sum. Convenience for systems that want to apply an impulse (knockback, wind, explosion force) on top of whatever velocity the entity already has.

**Parameters** \
`entity` [Entity](../../Bang/Entities/Entity.html) \
`addVelocity` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

#### CanSeeEntity(World, Vector2, Vector2, int, int)

```csharp
public static bool CanSeeEntity(World world, Vector2 from, Vector2 to, int selfEntityId, int targetEntityId)
```

Returns whether `from` can see the entity `targetEntityId` before the ray reaches `to`, by casting against the `CollisionLayersBase.ACTOR` layer (ignoring `selfEntityId`) and checking whether the first thing hit is `targetEntityId`. Used by AI to check whether a specific target is actually visible (not blocked by another actor or by the environment) rather than just checking for any line-of-sight blocker.

**Parameters** \
`world` [World](../../Bang/World.html) \
`from` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`to` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`selfEntityId` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`targetEntityId` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### CollidesAt(World, Entity, Vector2, int)

```csharp
public static bool CollidesAt(World world, Entity e, Vector2 position, int layerMask)
```

Returns whether `e`'s collider, hypothetically placed at `position`, would overlap a tile or another entity on `layerMask`. If `e` has no `ColliderComponent`, a temporary single-point collider is used (with a logged warning, since this is usually a sign the caller should have a real collider). The higher-level, per-call convenience overload of the more granular `CollidesAt(World, in Map, ...)` — prefer this one unless you're already holding a pre-filtered candidate list and want to avoid re-fetching it every call.

**Parameters** \
`world` [World](../../Bang/World.html) \
`e` [Entity](../../Bang/Entities/Entity.html) \
`position` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`layerMask` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### CollidesAt(World, Map, int, ColliderComponent, Vector2, Vector2, IList&lt;PhysicEntityCachedInfo&gt;, int, out int)

```csharp
public static bool CollidesAt(World world, in Map map, int ignoreId, ColliderComponent collider, Vector2 position, Vector2 scale, IList<PhysicEntityCachedInfo> others, int mask, out int hitId)
```

Lower-level overlap check: tests `collider` at `position`/`scale` against tile collisions in `map` first, then against the pre-filtered `others` list (as produced by the `FilterPositionAndColliderEntities` family), skipping `ignoreId`. Outputs the id of the first colliding entity via `hitId` (`-1` if only a tile was hit or nothing collided). Used internally by `CollidesAt(World, Entity, Vector2, int)` and `FindNextAvailablePosition`; call this directly when you already have a cached `others` list and want to avoid re-filtering it on every position tested.

**Parameters** \
`world` [World](../../Bang/World.html) \
`map` [Map](../../Murder/Core/Map.html) \
`ignoreId` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`collider` [ColliderComponent](../../Murder/Components/ColliderComponent.html) \
`position` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`scale` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`others` `IList<PhysicEntityCachedInfo>` \
`mask` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`hitId` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### CollidesAtPoint(World, Vector2, int)

```csharp
public static bool CollidesAtPoint(World world, Vector2 position, int layerMask)
```

Checks whether `position` (a single point, not a shape) collides with the map or any entity with a collider whose polygon contains that point, filtered by `layerMask`. Outputs the center of the colliding entity/tile conceptually (see remarks in source: the `hitId` output is computed but not currently returned to the caller). Use for point-sampling queries — e.g. "is this exact pixel inside a wall or hazard" — rather than shape-vs-shape overlap.

**Parameters** \
`world` [World](../../Bang/World.html) \
`position` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`layerMask` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### CollidesAtTile(Map, ColliderComponent, Vector2, int)

```csharp
public static bool CollidesAtTile(in Map map, ColliderComponent collider, Vector2 position, int mask)
```

Returns `true` if any shape in `collider`, placed at `position`, overlaps a tile flagged with `mask` in `map`. Tile-only counterpart to `CollidesWith`; used as the first, cheap check inside `CollidesAt` before testing against other entities.

**Parameters** \
`map` [Map](../../Murder/Core/Map.html) \
`collider` [ColliderComponent](../../Murder/Components/ColliderComponent.html) \
`position` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`mask` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### CollidesTile(World, Vector2, int)

```csharp
public static bool CollidesTile(World world, Vector2 position, int layerMask)
```

Simplified tile-only check: returns `true` if the single map tile under `position` is flagged with `layerMask`. Unlike `CollidesAtTile`, this does not consider a collider's shape at all — it only samples the one tile cell that `position` falls into. Useful for quick "is this point walkable" queries.

**Parameters** \
`world` [World](../../Bang/World.html) \
`position` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`layerMask` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### CollidesWith(Entity, Entity)

```csharp
public static bool CollidesWith(Entity entityA, Entity entityB)
```

Returns `true` if `entityA` and `entityB` currently overlap, using each entity's live global position and collider shapes. Returns `false` if either entity lacks a collider or a resolvable global position.

**Parameters** \
`entityA` [Entity](../../Bang/Entities/Entity.html) \
`entityB` [Entity](../../Bang/Entities/Entity.html) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### CollidesWith(Entity, Entity, Vector2)

```csharp
public static bool CollidesWith(Entity entityA, Entity entityB, Vector2 positionA)
```

Returns `true` if `entityA`, hypothetically placed at `positionA`, would overlap `entityB` at `entityB`'s current position. Use this variant when testing a candidate/next position for `entityA` (e.g. before committing a movement) rather than its current position.

**Parameters** \
`entityA` [Entity](../../Bang/Entities/Entity.html) \
`entityB` [Entity](../../Bang/Entities/Entity.html) \
`positionA` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### CollidesWith(IShape, Point, Vector2, IShape, Point, Vector2)

```csharp
public static bool CollidesWith(IShape shape1, Point position1, Vector2 scale1, IShape shape2, Point position2, Vector2 scale2)
```

The lowest-level shape-overlap test: returns `true` if `shape1` (at `position1`/`scale1`) overlaps `shape2` (at `position2`/`scale2`), dispatching to a specialised routine per shape-type pairing (polygon-vs-polygon, polygon-vs-box, lazy-vs-lazy, etc.) for performance. Every other collision-testing method in this class eventually narrows down to this call per pair of shapes.

**Parameters** \
`shape1` [IShape](../../Murder/Core/Geometry/IShape.html) \
`position1` [Point](../../Murder/Core/Geometry/Point.html) \
`scale1` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`shape2` [IShape](../../Murder/Core/Geometry/IShape.html) \
`position2` [Point](../../Murder/Core/Geometry/Point.html) \
`scale2` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### ConeCheck(World, Vector2, float, float, float, int)

```csharp
public static IEnumerable<Entity> ConeCheck(World world, Vector2 coneStart, float range, float angle, float angleRange, int collisionLayer)
```

Yields every entity on `collisionLayer` whose collider overlaps a cone shape with its tip at `coneStart`, pointing in direction `angle` (radians), reaching out `range` pixels, and spanning `angleRange` radians total. Used for melee swing/attack hitboxes and vision cones — anything that needs to detect entities within a wedge-shaped area rather than a circle or rectangle.

**Parameters** \
`world` [World](../../Bang/World.html) \
`coneStart` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`range` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`angle` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`angleRange` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`collisionLayer` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

**Returns** \
[IEnumerable\<Entity\>](../../Bang/Entities/Entity.html) \

#### ContainsPoint(Entity, Point)

```csharp
public static bool ContainsPoint(Entity entity, Point point)
```

Returns `true` if `point` falls inside any of `entity`'s collider shapes, evaluated with a per-shape-type test (circle/lazy radius check, box rectangle containment, polygon containment, etc.) rather than the general MTV/overlap machinery. Returns `false` if the entity has no collider. Handy for hit-testing a single point — e.g. a mouse click or a cursor — against an entity, as opposed to testing two shapes against each other.

**Parameters** \
`entity` [Entity](../../Bang/Entities/Entity.html) \
`point` [Point](../../Murder/Core/Geometry/Point.html) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### FilterPositionAndColliderEntities(List&lt;NodeInfo&lt;Entity&gt;&gt;, HashSet&lt;int&gt;, int, List&lt;PhysicEntityCachedInfo&gt;)

```csharp
public static void FilterPositionAndColliderEntities(List<NodeInfo<Entity>> entities, HashSet<int> ignore, int layerMask, List<PhysicEntityCachedInfo> result)
```

Filters a pre-fetched quadtree node list `entities` down to those that are active, not in `ignore`, have a `ColliderComponent`, and match `layerMask`, appending a `PhysicEntityCachedInfo` snapshot of each into `result`. All of the `FilterPositionAndColliderEntities` overloads follow the same output-parameter pattern (they populate a caller-owned `List`, rather than allocating and returning a new collection) so hot paths like collision resolution can reuse a single buffer across many calls per frame instead of allocating every time.

**Parameters** \
`entities` `List<NodeInfo<Entity>>` \
`ignore` [HashSet\<int\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Generic.HashSet-1?view=net-7.0) \
`layerMask` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`result` `List<PhysicEntityCachedInfo>` \

#### FilterPositionAndColliderEntities(IEnumerable&lt;Entity&gt;, int, List&lt;PhysicEntityCachedInfo&gt;)

```csharp
public static void FilterPositionAndColliderEntities(IEnumerable<Entity> entities, int layerMask, List<PhysicEntityCachedInfo> result)
```

Filters an already-known collection of `entities` down to those active with a collider matching `layerMask`, appending a `PhysicEntityCachedInfo` snapshot of each into `result`. Use this overload when you already hold a specific set of candidate entities (rather than wanting to search the whole world or quadtree).

**Parameters** \
`entities` [IEnumerable\<Entity\>](../../Bang/Entities/Entity.html) \
`layerMask` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`result` `List<PhysicEntityCachedInfo>` \

#### FilterPositionAndColliderEntities(World, Func&lt;Entity, bool&gt;, List&lt;PhysicEntityCachedInfo&gt;)

```csharp
public static void FilterPositionAndColliderEntities(World world, Func<Entity, bool> filter, List<PhysicEntityCachedInfo> result)
```

Clears `result`, then fills it with a `PhysicEntityCachedInfo` snapshot of every entity in `world` that has both a collider and position component and satisfies the custom `filter` predicate. Use when layer masking alone isn't specific enough and you need arbitrary per-entity logic to decide inclusion.

**Parameters** \
`world` [World](../../Bang/World.html) \
`filter` [Func\<Entity, bool\>](https://learn.microsoft.com/en-us/dotnet/api/System.Func-2?view=net-7.0) \
`result` `List<PhysicEntityCachedInfo>` \

#### FilterPositionAndColliderEntities(World, int, List&lt;PhysicEntityCachedInfo&gt;)

```csharp
public static void FilterPositionAndColliderEntities(World world, int layerMask, List<PhysicEntityCachedInfo> result)
```

Clears `result`, then fills it with a `PhysicEntityCachedInfo` snapshot of every entity in `world` that has a collider and position and matches `layerMask`. This is the overload most collision code uses to gather a candidate list before running per-position overlap checks with `CollidesAt`/`GetFirstMtvAt`/`GetMtvAt`.

**Parameters** \
`world` [World](../../Bang/World.html) \
`layerMask` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`result` `List<PhysicEntityCachedInfo>` \

#### FilterPositionAndColliderEntities(World, int, Type[], List&lt;(int, ColliderComponent, Vector2)&gt;)

```csharp
public static void FilterPositionAndColliderEntities(World world, int layerMask, Type[]? requireComponents, List<(int id, ColliderComponent collider, Vector2 position)> result)
```

Fills `result` with `(entityId, collider, position)` tuples for every entity whose collider layer differs from `layerMask` (note: this overload filters on inequality, not a bitmask match) and, if `requireComponents` is supplied, also requires the entity to have every one of those additional component types. Used by editor/gizmo-style tooling that needs the raw collider + position data for a broader entity set than the standard `PhysicEntityCachedInfo` snapshot covers.

**Parameters** \
`world` [World](../../Bang/World.html) \
`layerMask` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`requireComponents` [Type[]](https://learn.microsoft.com/en-us/dotnet/api/System.Type?view=net-7.0) \
`result` `List<(int, ColliderComponent, Vector2)>` \

#### FindClosestEntityOnRange(World, Vector2, float, int, HashSet&lt;int&gt;, out Entity, out Vector2)

```csharp
public static bool FindClosestEntityOnRange(World world, Vector2 fromPosition, float range, int collisionLayer, HashSet<int> excludeEntities, out Entity? target, out Vector2? location)
```

Searches the quadtree for the nearest entity on `collisionLayer` within `range` of `fromPosition`, skipping any id present in `excludeEntities`; outputs the found `target` and its `location` (both `null` if nothing was found within range), and returns whether a target was found. Used by AI targeting logic to pick the nearest valid enemy/interactable within a search radius.

**Parameters** \
`world` [World](../../Bang/World.html) \
`fromPosition` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`range` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`collisionLayer` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`excludeEntities` [HashSet\<int\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Generic.HashSet-1?view=net-7.0) \
`target` [Entity?](../../Bang/Entities/Entity.html) \
`location` [Vector2?](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### FindNextAvailablePosition(World, Entity, Vector2, Vector2, int, NextAvailablePositionFlags)

```csharp
public static Vector2? FindNextAvailablePosition(World world, Entity e, Vector2 center, Vector2 target, int layerMask, NextAvailablePositionFlags flags = NextAvailablePositionFlags.CheckTarget | NextAvailablePositionFlags.CheckNeighbours | NextAvailablePositionFlags.CheckRecursiveNeighbours)
```

Finds an unoccupied position for entity `e` near `target` on `layerMask`, checking the exact target first and then breadth-first expanding to neighbouring grid cells (up to an internal depth limit of 5) when `NextAvailablePositionFlags.CheckNeighbours` is set. Returns `null` if no free position was found within the search depth. Use this to safely place or reposition an entity — e.g. spawning a companion next to the player, or resolving a pushed entity into free space — instead of manually looping over candidate offsets.

**Parameters** \
`world` [World](../../Bang/World.html) \
`e` [Entity](../../Bang/Entities/Entity.html) \
`center` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`target` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`layerMask` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`flags` [NextAvailablePositionFlags](../../Murder/Services/NextAvailablePositionFlags.html) \

**Returns** \
[Vector2?](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

#### GetAllCollisionsAt(World, Point, Vector2, ColliderComponent, int, int)

```csharp
public static IEnumerable<Entity> GetAllCollisionsAt(World world, Point position, Vector2 scale, ColliderComponent collider, int ignoreId, int mask)
```

Yields every active, non-destroyed entity on `mask` whose collider overlaps `collider` when placed at `position`/`scale`, excluding `ignoreId`. Queries the world's quadtree for broad-phase candidates before doing the precise shape test. Use to enumerate everything currently touching a hypothetical collider placement, e.g. to apply an area-of-effect to everything inside it.

**Parameters** \
`world` [World](../../Bang/World.html) \
`position` [Point](../../Murder/Core/Geometry/Point.html) \
`scale` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`collider` [ColliderComponent](../../Murder/Components/ColliderComponent.html) \
`ignoreId` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`mask` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

**Returns** \
[IEnumerable\<Entity\>](../../Bang/Entities/Entity.html) \

#### GetAllCollisionsAtGrid(World, Point, List&lt;NodeInfo&lt;Entity&gt;&gt;)

```csharp
public static void GetAllCollisionsAtGrid(World world, Point grid, ref List<NodeInfo<Entity>> output)
```

Populates `output` with every quadtree entry whose bounding box touches the rectangle covered by grid cell `grid`. Not cached or especially fast (per the source comment); prefer the entity-level query methods for anything performance sensitive, and reserve this for one-off tile-level lookups such as editor tooling.

**Parameters** \
`world` [World](../../Bang/World.html) \
`grid` [Point](../../Murder/Core/Geometry/Point.html) \
`output` `List<NodeInfo<Entity>>` \

#### GetBoundingBox(ColliderComponent, Vector2, Vector2)

```csharp
public static Rectangle GetBoundingBox(this ColliderComponent collider, Vector2 position, Vector2 scale)
```

Returns the combined float bounding rectangle of every shape in `collider`, placed at `position` and scaled by `scale` (correctly handling negative scale as a flip). Returns `Rectangle.Empty` if the collider has no shapes.

**Parameters** \
`collider` [ColliderComponent](../../Murder/Components/ColliderComponent.html) \
`position` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`scale` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

**Returns** \
[Rectangle](../../Murder/Core/Geometry/Rectangle.html) \

#### GetCarveBoundingBox(ColliderComponent, Vector2, Vector2)

```csharp
public static IntRectangle GetCarveBoundingBox(this ColliderComponent collider, Vector2 position, Vector2 scale)
```

Returns the integer bounding box used when this collider "carves" a hole into the tilemap's navigation/occupancy data, shrinking the box slightly (`occupiedThreshold: .75f`) so a shape only carves tiles it substantially overlaps rather than every tile it merely touches at the edge.

**Parameters** \
`collider` [ColliderComponent](../../Murder/Components/ColliderComponent.html) \
`position` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`scale` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

**Returns** \
[IntRectangle](../../Murder/Core/Geometry/IntRectangle.html) \

#### GetColliderBoundingBox(Entity)

```csharp
public static IntRectangle GetColliderBoundingBox(this Entity target)
```

Returns the integer bounding box of `target`'s collider at its current global position and scale, or `IntRectangle.Empty` if `target` lacks a collider or position component. Convenience wrapper over `GetBoundingBox` for the common case of "give me this entity's on-screen/on-grid footprint".

**Parameters** \
`target` [Entity](../../Bang/Entities/Entity.html) \

**Returns** \
[IntRectangle](../../Murder/Core/Geometry/IntRectangle.html) \

#### GetCollidersBoundingBox(ColliderComponent, Point, bool)

```csharp
public static IntRectangle[] GetCollidersBoundingBox(this ColliderComponent collider, Point position, bool gridCoordinates)
```

Returns one bounding box per shape in `collider` (rather than one combined box), each placed at `position`; when `gridCoordinates` is `true`, boxes are floored/ceiled to grid-cell boundaries instead of raw pixels. Use when you need per-shape (not just overall) bounds, e.g. drawing debug outlines for a multi-shape collider.

**Parameters** \
`collider` [ColliderComponent](../../Murder/Components/ColliderComponent.html) \
`position` [Point](../../Murder/Core/Geometry/Point.html) \
`gridCoordinates` [bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

**Returns** \
[IntRectangle[]](../../Murder/Core/Geometry/IntRectangle.html) \

#### GetFirstMtv(int, ColliderComponent, Vector2, IList&lt;PhysicEntityCachedInfo&gt;, out int)

```csharp
public static Vector2 GetFirstMtv(int entityId, ColliderComponent collider, Vector2 position, IList<PhysicEntityCachedInfo> others, out int hitId)
```

Returns the minimum translation vector needed to push `collider` (owned by `entityId`, at `position`) out of the *first* overlap found against `others`, and outputs the id of that entity. Unlike `GetMtvAt`, which accumulates every overlap into a list, this stops at the first hit — cheaper when you only need to resolve one collision at a time.

**Parameters** \
`entityId` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`collider` [ColliderComponent](../../Murder/Components/ColliderComponent.html) \
`position` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`others` `IList<PhysicEntityCachedInfo>` \
`hitId` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

**Returns** \
[Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

#### GetFirstMtvAt(Map, ColliderComponent, Vector2, Vector2, IList&lt;PhysicEntityCachedInfo&gt;, int, out int, out int, out Vector2)

```csharp
public static bool GetFirstMtvAt(in Map map, ColliderComponent collider, Vector2 fromPosition, Vector2 toPosition, IList<PhysicEntityCachedInfo> others, int mask, out int hitId, out int layer, out Vector2 mtv)
```

Checks for collision when `collider` moves from `fromPosition` to `toPosition` — against both tile collisions in `map` and entities in `others` — and accumulates a combined minimum-translation-vector `mtv` that would resolve every overlap found (favouring the closest hit for `hitId`/`layer`). This is the core primitive behind push-out/collision-resolution movement: call it after tentatively moving an entity to compute how far (and in what direction) to correct the position to eliminate overlap.

**Parameters** \
`map` [Map](../../Murder/Core/Map.html) \
`collider` [ColliderComponent](../../Murder/Components/ColliderComponent.html) \
`fromPosition` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`toPosition` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`others` `IList<PhysicEntityCachedInfo>` \
`mask` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`hitId` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`layer` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`mtv` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### GetMtvAt(Map, int, ColliderComponent, Vector2, IEnumerable&lt;PhysicEntityCachedInfo&gt;, int, out int)

```csharp
public static List<Vector2> GetMtvAt(in Map map, int ignoreId, ColliderComponent collider, Vector2 position, IEnumerable<PhysicEntityCachedInfo> others, int mask, out int hitId)
```

Returns a list containing every individual minimum-translation-vector found for `collider` at `position` — one per overlapping tile plus one per overlapping shape in `others` (excluding `ignoreId`) — rather than a single combined vector like `GetFirstMtvAt`. Use when a caller wants to inspect or weigh each individual overlap separately instead of a pre-summed resolution vector.

**Parameters** \
`map` [Map](../../Murder/Core/Map.html) \
`ignoreId` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`collider` [ColliderComponent](../../Murder/Components/ColliderComponent.html) \
`position` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`others` [IEnumerable\<PhysicEntityCachedInfo\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Generic.IEnumerable-1?view=net-7.0) \
`mask` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`hitId` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

**Returns** \
[List\<Vector2\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Generic.List-1?view=net-7.0) \

#### HasCachedCollisionWith(Entity, int)

```csharp
public static bool HasCachedCollisionWith(Entity entity, int entityId)
```

Returns whether `entity`'s `CollisionCacheComponent` currently records an active collision with `entityId`. Used by trigger systems (e.g. `TriggerCollisionSystem`) to check whether a collision they previously recorded via `AddToCollisionCache` is still ongoing.

**Parameters** \
`entity` [Entity](../../Bang/Entities/Entity.html) \
`entityId` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### HasLineOfSight(World, Entity, Entity, int)

```csharp
public static bool HasLineOfSight(World world, Entity from, Entity to, int mask)
```

Returns `true` if no tile or entity on `mask` blocks the straight line between `from` and `to`'s current global positions (both entities themselves are ignored so they don't block their own check). Prefer this entity-based overload over the raw `Vector2` one when you already have both entities, since it also excludes their own colliders automatically.

**Parameters** \
`world` [World](../../Bang/World.html) \
`from` [Entity](../../Bang/Entities/Entity.html) \
`to` [Entity](../../Bang/Entities/Entity.html) \
`mask` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### HasLineOfSight(World, Vector2, Vector2)

```csharp
public static bool HasLineOfSight(World world, Vector2 from, Vector2 to)
```

Returns `true` if nothing on the `CollisionLayersBase.BLOCK_VISION` layer blocks the straight line between `from` and `to`. The default, vision-specific overload of `HasLineOfSight(World, Vector2, Vector2, int)`.

**Parameters** \
`world` [World](../../Bang/World.html) \
`from` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`to` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### HasLineOfSight(World, Vector2, Vector2, int)

```csharp
public static bool HasLineOfSight(World world, Vector2 from, Vector2 to, int mask)
```

Returns `true` if a `Raycast` on `mask` between `from` and `to` finds nothing in the way. The general-purpose, mask-parameterised primitive that `HasLineOfSight(World, Vector2, Vector2)` and `HasSolidLineOfSight` both delegate to.

**Parameters** \
`world` [World](../../Bang/World.html) \
`from` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`to` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`mask` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### HasSolidLineOfSight(World, Vector2, Vector2)

```csharp
public static bool HasSolidLineOfSight(World world, Vector2 from, Vector2 to)
```

Returns `true` if nothing on the `CollisionLayersBase.SOLID` layer blocks the straight line between `from` and `to`. Use this instead of `HasLineOfSight(World, Vector2, Vector2)` when the check is about physical/movement obstruction rather than vision (e.g. can a projectile physically travel this path, as opposed to can an AI see along it).

**Parameters** \
`world` [World](../../Bang/World.html) \
`from` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`to` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### IsCollidingWith(Entity, Entity)

```csharp
public static bool IsCollidingWith(this Entity a, Entity b)
```

Returns whether `a`'s `CollisionCacheComponent` currently lists `b` as colliding — a cheap, cached lookup (`HasCachedCollisionWith` under a different name/signature) rather than a live shape test. Use when you only need to know about a collision that a trigger system already detected and recorded this frame, not to perform a fresh overlap check.

**Parameters** \
`a` [Entity](../../Bang/Entities/Entity.html) \
`b` [Entity](../../Bang/Entities/Entity.html) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### Neighbours(Vector2, World, float)

```csharp
public static IEnumerable<Vector2> Neighbours(this Vector2 position, World world, float unit)
```

Yields the neighbouring positions of `position`, spaced `unit` grid cells apart, clamped to the bounds of `world`'s map (falling back to a 256x256 default if the world has no `MapComponent` yet). This does not check for collision — it purely enumerates candidate nearby points; callers such as `FindNextAvailablePosition` are responsible for testing each one.

**Parameters** \
`position` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`world` [World](../../Bang/World.html) \
`unit` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

**Returns** \
[IEnumerable\<Vector2\>](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

#### Raycast(World, Vector2, Vector2, int, IEnumerable&lt;int&gt;, out RaycastHit)

```csharp
public static bool Raycast(World world, Vector2 startPosition, Vector2 endPosition, int layerMask, IEnumerable<int> ignoreEntities, out RaycastHit hit)
```

Casts a ray from `startPosition` to `endPosition`, testing first against tiles (via `RaycastTiles`) and then against every candidate entity on `layerMask` found in the world's quadtree along the ray's bounding box (skipping ids in `ignoreEntities` and their children), returning the *closest* intersection in `hit`. This is the main raycasting entry point — use it for hit-scan weapons, vision checks, and any "what's the first thing between A and B" query. Entities whose collider layer includes `CollisionLayersBase.RAYIGNORE` are always skipped.

**Parameters** \
`world` [World](../../Bang/World.html) \
`startPosition` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`endPosition` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`layerMask` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`ignoreEntities` [IEnumerable\<int\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Generic.IEnumerable-1?view=net-7.0) \
`hit` [RaycastHit](../../Murder/Services/RaycastHit.html) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### Raycast(World, Vector2, Vector2, float, int, IEnumerable&lt;int&gt;, out RaycastHit)

```csharp
public static bool Raycast(World world, Vector2 startPosition, Vector2 endPosition, float minHitDistance, int layerMask, IEnumerable<int> ignoreEntities, out RaycastHit hit)
```

Same as `Raycast(World, Vector2, Vector2, int, IEnumerable<int>, out RaycastHit)`, but first nudges the start point `minHitDistance` units toward `endPosition` before casting. Use to avoid the ray immediately re-hitting the caster's own collider edge (e.g. for a projectile fired from just inside the shooter's hitbox).

**Parameters** \
`world` [World](../../Bang/World.html) \
`startPosition` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`endPosition` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`minHitDistance` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`layerMask` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`ignoreEntities` [IEnumerable\<int\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Generic.IEnumerable-1?view=net-7.0) \
`hit` [RaycastHit](../../Murder/Services/RaycastHit.html) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### RaycastTiles(World, Vector2, Vector2, int, out RaycastHit)

```csharp
public static bool RaycastTiles(World world, Vector2 startPos, Vector2 endPos, int flags, out RaycastHit hit)
```

Casts a ray from `startPos` to `endPos` purely against map tiles (no entities), using a DDA grid-traversal algorithm to walk cell-by-cell and stop at the first tile whose flags overlap `flags`. Called internally by `Raycast` before it tests entities, but can be used directly when only tile collision matters (e.g. checking whether a straight path is blocked by walls, ignoring actors).

**Parameters** \
`world` [World](../../Bang/World.html) \
`startPos` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`endPos` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`flags` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`hit` [RaycastHit](../../Murder/Services/RaycastHit.html) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### RemoveFromCollisionCache(Entity, int)

```csharp
public static bool RemoveFromCollisionCache(Entity entity, int entityId)
```

Removes `entityId` from `entity`'s `CollisionCacheComponent`, returning `true` if it was present (and thus removed). This is usually handled automatically by `TriggerPhysics`-style systems, since a collision-exit message typically needs to be sent at the same moment the id is removed — call it directly only if you're implementing custom trigger/exit logic.

**Parameters** \
`entity` [Entity](../../Bang/Entities/Entity.html) \
`entityId` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### TryGetMap(World)

```csharp
public static Map? TryGetMap(World world)
```

Returns `world`'s unique `MapComponent`'s `Map`, or `null` if the world doesn't have one yet. Null-safe alternative to calling `world.GetUniqueMap().Map` directly when the map might not exist (e.g. very early in world setup).

**Parameters** \
`world` [World](../../Bang/World.html) \

**Returns** \
[Map?](../../Murder/Core/Map.html) \

⚡
