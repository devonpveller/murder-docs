# PhysicsServices

**Namespace:** Murder.Services \
**Assembly:** Murder.dll

```csharp
public static class PhysicsServices
```

Provides collision detection, raycasting, overlap queries, and physics utility methods for the Murder ECS world.

**Intent:** Centralises all physics and spatial query operations so game systems can test collisions and find entities in the world without manual component iteration.

**Use-case:** Use `Raycast` for projectile line-of-sight checks, `GetAllCollisionsAt` for overlap detection, `FilterPositionAndColliderEntities` to query collidable entities by layer, and `FindNextAvailablePosition` to safely place entities without overlapping obstacles.

### ⭐ Methods
#### CanSeeEntity(World, Vector2, Vector2, int, int)
```csharp
public bool CanSeeEntity(World world, Vector2 from, Vector2 to, int selfEntityId, int targetEntityId)
```

Returns whether <paramref name="from" /> an see an entity <paramref name="targetEntityId" /> before
            it gets to <paramref name="to" />.

**Parameters** \
`world` [World](../../Bang/World.html) \
`from` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`to` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`selfEntityId` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`targetEntityId` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### CollidesAt(Map&, int, ColliderComponent, Vector2, ImmutableArray<T>, int, out Int32&)
```csharp
public bool CollidesAt(Map& map, int ignoreId, ColliderComponent collider, Vector2 position, ImmutableArray<T> others, int mask, Int32& hitId)
```
Tests whether `collider` at `position` overlaps any entity in `others` (excluding `ignoreId`) with the given layer `mask`, and outputs the first hit entity ID.

**Parameters** \
`map` [Map&](../../Murder/Core/Map.html) \
`ignoreId` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`collider` [ColliderComponent](../../Murder/Components/ColliderComponent.html) \
`position` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`others` [ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \
`mask` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`hitId` [int&](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### CollidesAtTile(Map&, ColliderComponent, Vector2, int)
```csharp
public bool CollidesAtTile(Map& map, ColliderComponent collider, Vector2 position, int mask)
```
Returns `true` if `collider` at `position` overlaps a tile with the given collision layer `mask`.

**Parameters** \
`map` [Map&](../../Murder/Core/Map.html) \
`collider` [ColliderComponent](../../Murder/Components/ColliderComponent.html) \
`position` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`mask` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### CollidesWith(Entity, Entity, Vector2)
```csharp
public bool CollidesWith(Entity entityA, Entity entityB, Vector2 positionA)
```
Returns `true` if `entityA` (tested at `positionA`) overlaps `entityB` using their collider shapes.

**Parameters** \
`entityA` [Entity](../../Bang/Entities/Entity.html) \
`entityB` [Entity](../../Bang/Entities/Entity.html) \
`positionA` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### CollidesWith(Entity, Entity)
```csharp
public bool CollidesWith(Entity entityA, Entity entityB)
```
Returns `true` if `entityA` and `entityB` currently overlap using their world-position collider shapes.

**Parameters** \
`entityA` [Entity](../../Bang/Entities/Entity.html) \
`entityB` [Entity](../../Bang/Entities/Entity.html) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### CollidesWith(IShape, Point, IShape, Point)
```csharp
public bool CollidesWith(IShape shape1, Point position1, IShape shape2, Point position2)
```
Returns `true` if two arbitrary shapes overlap when placed at their respective positions.

**Parameters** \
`shape1` [IShape](../../Murder/Core/Geometry/IShape.html) \
`position1` [Point](../../Murder/Core/Geometry/Point.html) \
`shape2` [IShape](../../Murder/Core/Geometry/IShape.html) \
`position2` [Point](../../Murder/Core/Geometry/Point.html) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### ContainsPoint(Entity, Point)
```csharp
public bool ContainsPoint(Entity entity, Point point)
```
Returns `true` if `point` falls inside any of the entity's collider shapes.

**Parameters** \
`entity` [Entity](../../Bang/Entities/Entity.html) \
`point` [Point](../../Murder/Core/Geometry/Point.html) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### FindClosestEntityOnRange(World, Vector2, float, int, HashSet<T>, out Entity&, out Nullable`1&)
```csharp
public bool FindClosestEntityOnRange(World world, Vector2 fromPosition, float range, int collisionLayer, HashSet<T> excludeEntities, Entity& target, Nullable`1& location)
```
Searches for the nearest entity within `range` on the given collision layer, skipping any in `excludeEntities`; populates `target` and `location` on success.

**Parameters** \
`world` [World](../../Bang/World.html) \
`fromPosition` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`range` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`collisionLayer` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`excludeEntities` [HashSet\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Generic.HashSet-1?view=net-7.0) \
`target` [Entity&](../../Bang/Entities/Entity.html) \
`location` [T?&](https://learn.microsoft.com/en-us/dotnet/api/System.Nullable-1?view=net-7.0) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### GetFirstMtvAt(Map&, HashSet<T>, ColliderComponent, Vector2, ImmutableArray<T>, int, out Int32&, out Int32&, out Vector2&)
```csharp
public bool GetFirstMtvAt(Map& map, HashSet<T> ignoreIds, ColliderComponent collider, Vector2 position, ImmutableArray<T> others, int mask, Int32& hitId, Int32& layer, Vector2& mtv)
```
Finds the first overlap and computes the minimum translation vector (MTV) needed to resolve it, outputting the hit entity ID, its layer, and the MTV.

**Parameters** \
`map` [Map&](../../Murder/Core/Map.html) \
`ignoreIds` [HashSet\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Generic.HashSet-1?view=net-7.0) \
`collider` [ColliderComponent](../../Murder/Components/ColliderComponent.html) \
`position` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`others` [ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \
`mask` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`hitId` [int&](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`layer` [int&](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`mtv` [Vector2&](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### HasCachedCollisionWith(Entity, int)
```csharp
public bool HasCachedCollisionWith(Entity entity, int entityId)
```

Check if a trigger is colliding with an actor via the TriggerCollisionSystem.

**Parameters** \
`entity` [Entity](../../Bang/Entities/Entity.html) \
\
`entityId` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
\

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### HasLineOfSight(World, Entity, Entity)
```csharp
public bool HasLineOfSight(World world, Entity from, Entity to)
```
Returns `true` if no tile or solid entity blocks the straight line between `from` and `to`.

**Parameters** \
`world` [World](../../Bang/World.html) \
`from` [Entity](../../Bang/Entities/Entity.html) \
`to` [Entity](../../Bang/Entities/Entity.html) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### HasLineOfSight(World, Vector2, Vector2)
```csharp
public bool HasLineOfSight(World world, Vector2 from, Vector2 to)
```
Returns `true` if no tile or solid entity blocks the straight line between the two world positions.

**Parameters** \
`world` [World](../../Bang/World.html) \
`from` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`to` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### Raycast(World, Vector2, Vector2, int, IEnumerable<T>, out RaycastHit&)
```csharp
public bool Raycast(World world, Vector2 startPosition, Vector2 endPosition, int layerMask, IEnumerable<T> ignoreEntities, RaycastHit& hit)
```
Casts a ray from `startPosition` to `endPosition`, testing against entities with the given layer mask; populates `hit` with the first intersection found.

**Parameters** \
`world` [World](../../Bang/World.html) \
`startPosition` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`endPosition` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`layerMask` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`ignoreEntities` [IEnumerable\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Generic.IEnumerable-1?view=net-7.0) \
`hit` [RaycastHit&](../../Murder/Services/RaycastHit.html) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### RaycastTiles(World, Vector2, Vector2, int, out RaycastHit&)
```csharp
public bool RaycastTiles(World world, Vector2 startPosition, Vector2 endPosition, int flags, RaycastHit& hit)
```

**Parameters** \
`world` [World](../../Bang/World.html) \
`startPosition` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`endPosition` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`flags` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`hit` [RaycastHit&](../../Murder/Services/RaycastHit.html) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### RemoveFromCollisionCache(Entity, int)
```csharp
public bool RemoveFromCollisionCache(Entity entity, int entityId)
```

Removes an ID from the IsColliding component. This is usually handled by TriggerPhysics system, since a message must be sent when exiting a collision.

**Parameters** \
`entity` [Entity](../../Bang/Entities/Entity.html) \
\
`entityId` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
\

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
\

#### ConeCheck(World, Vector2, float, float, float, int)
```csharp
public IEnumerable<T> ConeCheck(World world, Vector2 coneStart, float range, float angle, float angleRange, int collisionLayer)
```

Checks for collisions in a cone.

**Parameters** \
`world` [World](../../Bang/World.html) \
`coneStart` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`range` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`angle` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`angleRange` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`collisionLayer` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

**Returns** \
[IEnumerable\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Generic.IEnumerable-1?view=net-7.0) \

#### GetAllCollisionsAt(World, Point, ColliderComponent, int, int)
```csharp
public IEnumerable<T> GetAllCollisionsAt(World world, Point position, ColliderComponent collider, int ignoreId, int mask)
```
Returns all entities whose colliders overlap `collider` placed at `position`, filtered by layer `mask` and excluding `ignoreId`.

**Parameters** \
`world` [World](../../Bang/World.html) \
`position` [Point](../../Murder/Core/Geometry/Point.html) \
`collider` [ColliderComponent](../../Murder/Components/ColliderComponent.html) \
`ignoreId` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`mask` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

**Returns** \
[IEnumerable\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Generic.IEnumerable-1?view=net-7.0) \

#### Neighbours(Vector2, World, float)
```csharp
public IEnumerable<T> Neighbours(Vector2 position, World world, float unit)
```

Get all the neighbours of a position within the world.
            This does not check for collision (yet)!

**Parameters** \
`position` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`world` [World](../../Bang/World.html) \
`unit` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

**Returns** \
[IEnumerable\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Generic.IEnumerable-1?view=net-7.0) \

#### FilterEntities(World, int)
```csharp
public ImmutableArray<T> FilterEntities(World world, int layerMask)
```
Returns all entities in the world that have colliders matching `layerMask`.

**Parameters** \
`world` [World](../../Bang/World.html) \
`layerMask` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

**Returns** \
[ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \

#### FilterPositionAndColliderEntities(World, Func<T, TResult>)
```csharp
public ImmutableArray<T> FilterPositionAndColliderEntities(World world, Func<T, TResult> filter)
```
Returns all entities that have both a position and a collider component and satisfy the custom `filter` predicate.

**Parameters** \
`world` [World](../../Bang/World.html) \
`filter` [Func\<T, TResult\>](https://learn.microsoft.com/en-us/dotnet/api/System.Func-2?view=net-7.0) \

**Returns** \
[ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \

#### FilterPositionAndColliderEntities(World, int, Type[])
```csharp
public ImmutableArray<T> FilterPositionAndColliderEntities(World world, int layerMask, Type[] requireComponents)
```
Returns all entities matching `layerMask` that also possess all of the additional required component types.

**Parameters** \
`world` [World](../../Bang/World.html) \
`layerMask` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`requireComponents` [Type[]](https://learn.microsoft.com/en-us/dotnet/api/System.Type?view=net-7.0) \

**Returns** \
[ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \

#### FilterPositionAndColliderEntities(World, int)
```csharp
public ImmutableArray<T> FilterPositionAndColliderEntities(World world, int layerMask)
```
Returns all entities in the world that have both a position component and a collider matching `layerMask`.

**Parameters** \
`world` [World](../../Bang/World.html) \
`layerMask` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

**Returns** \
[ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \

#### FilterPositionAndColliderEntities(IEnumerable<T>, int)
```csharp
public ImmutableArray<T> FilterPositionAndColliderEntities(IEnumerable<T> entities, int layerMask)
```
Filters an existing entity collection, returning only those with a collider matching `layerMask`.

**Parameters** \
`entities` [IEnumerable\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Generic.IEnumerable-1?view=net-7.0) \
`layerMask` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

**Returns** \
[ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \

#### GetCarveBoundingBox(ColliderComponent, Vector2)
```csharp
public IntRectangle GetCarveBoundingBox(ColliderComponent collider, Vector2 position)
```
Returns the bounding rectangle used when this collider carves into the tilemap.

**Parameters** \
`collider` [ColliderComponent](../../Murder/Components/ColliderComponent.html) \
`position` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

**Returns** \
[IntRectangle](../../Murder/Core/Geometry/IntRectangle.html) \

#### GetColliderBoundingBox(Entity)
```csharp
public IntRectangle GetColliderBoundingBox(Entity target)
```

Get bounding box of an entity that contains both [ColliderComponent](../../Murder/Components/ColliderComponent.html)
            and [PositionComponent](../../Murder/Components/PositionComponent.html).

**Parameters** \
`target` [Entity](../../Bang/Entities/Entity.html) \

**Returns** \
[IntRectangle](../../Murder/Core/Geometry/IntRectangle.html) \

#### GetCollidersBoundingBox(ColliderComponent, Point, bool)
```csharp
public IntRectangle[] GetCollidersBoundingBox(ColliderComponent collider, Point position, bool gridCoordinates)
```
Returns per-shape bounding rectangles for all shapes in `collider` at `position`, optionally converted to grid coordinates.

**Parameters** \
`collider` [ColliderComponent](../../Murder/Components/ColliderComponent.html) \
`position` [Point](../../Murder/Core/Geometry/Point.html) \
`gridCoordinates` [bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

**Returns** \
[IntRectangle[]](../../Murder/Core/Geometry/IntRectangle.html) \

#### GetMtvAt(Map&, int, ColliderComponent, Vector2, IEnumerable<T>, int, out Int32&)
```csharp
public List<T> GetMtvAt(Map& map, int ignoreId, ColliderComponent collider, Vector2 position, IEnumerable<T> others, int mask, Int32& hitId)
```
Returns a list of all minimum translation vectors for each overlapping entity found.

**Parameters** \
`map` [Map&](../../Murder/Core/Map.html) \
`ignoreId` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`collider` [ColliderComponent](../../Murder/Components/ColliderComponent.html) \
`position` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`others` [IEnumerable\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Generic.IEnumerable-1?view=net-7.0) \
`mask` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`hitId` [int&](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

**Returns** \
[List\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Generic.List-1?view=net-7.0) \

#### GetBoundingBox(ColliderComponent, Vector2)
```csharp
public Rectangle GetBoundingBox(ColliderComponent collider, Vector2 position)
```
Returns the combined float bounding rectangle of all shapes in `collider` at `position`.

**Parameters** \
`collider` [ColliderComponent](../../Murder/Components/ColliderComponent.html) \
`position` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

**Returns** \
[Rectangle](../../Murder/Core/Geometry/Rectangle.html) \

#### FindNextAvailablePosition(World, Entity, Vector2, Vector2, int, NextAvailablePositionFlags)
```csharp
public T? FindNextAvailablePosition(World world, Entity e, Vector2 center, Vector2 target, int layerMask, NextAvailablePositionFlags flags)
```
Finds the nearest unoccupied position around `target` that is valid for entity `e`, using the search strategy specified by `flags`.

**Parameters** \
`world` [World](../../Bang/World.html) \
`e` [Entity](../../Bang/Entities/Entity.html) \
`center` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`target` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`layerMask` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`flags` [NextAvailablePositionFlags](../../Murder/Services/NextAvailablePositionFlags.html) \

**Returns** \
[T?](https://learn.microsoft.com/en-us/dotnet/api/System.Nullable-1?view=net-7.0) \

#### AddToCollisionCache(Entity, int)
```csharp
public void AddToCollisionCache(Entity entity, int entityId)
```
Adds `entityId` to the entity's `IsColliding` cache, indicating an active collision with that entity.

**Parameters** \
`entity` [Entity](../../Bang/Entities/Entity.html) \
`entityId` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### AddVelocity(Entity, Vector2)
```csharp
public void AddVelocity(Entity entity, Vector2 addVelocity)
```
Adds `addVelocity` to the entity's current velocity component.

**Parameters** \
`entity` [Entity](../../Bang/Entities/Entity.html) \
`addVelocity` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

#### GetAllCollisionsAtGrid(World, Point, List`1&)
```csharp
public void GetAllCollisionsAtGrid(World world, Point grid, List`1& output)
```
Populates `output` with all entities whose colliders touch the given grid cell.

**Parameters** \
`world` [World](../../Bang/World.html) \
`grid` [Point](../../Murder/Core/Geometry/Point.html) \
`output` [List\<T\>&](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Generic.List-1?view=net-7.0) \



⚡