# MapCarveCollisionSystem

**Namespace:** Murder.Systems \
**Assembly:** Murder.dll

```csharp
public class MapCarveCollisionSystem : IReactiveSystem, ISystem, IActivateAndDeactivateListenerSystem
```

Tracks entities with `CarveComponent` and `ColliderComponent` and updates the pathfinding/collision map whenever they are added, moved, removed, activated, or deactivated, carving out or restoring navigable grid cells.

**Intent:** Keeps the navigable area of the map accurate by dynamically carving dynamic obstacles (moving walls, doors, pushable crates) into the navigation grid, and un-carving them when they move away, are removed, or are deactivated.

**Use-case:** Attach `CarveComponent` alongside a `ColliderComponent` to any dynamic obstacle; this system keeps the pathfinding map up to date so agents automatically route around it. Only colliders that are `SOLID`/`PATHFIND` layer, or whose `CarveComponent` has `ClearPath` or `ApplyLayers` set, actually carve the grid (see `IsValidCarve`). Note that moving an already-carved entity (`OnModified`) updates the collision grid but does **not** trigger a pathfinding data refresh — only add/remove/activate/deactivate do.

**Implements:** _[IReactiveSystem](../../Bang/Systems/IReactiveSystem.html), [ISystem](../../Bang/Systems/ISystem.html), [IActivateAndDeactivateListenerSystem](../../Bang/Systems/IActivateAndDeactivateListenerSystem.html)_

### ⭐ Constructors

```csharp
public MapCarveCollisionSystem()
```

### ⭐ Methods

#### IsValidCarve(Entity, ColliderComponent, CarveComponent)

```csharp
protected bool IsValidCarve(Entity e, ColliderComponent collider, CarveComponent carve)
```

Returns whether the given entity should apply a carve to the map; override to add custom validity conditions.

**Parameters** \
`e` [Entity](../../Bang/Entities/Entity.html) \
`collider` [ColliderComponent](../../Murder/Components/ColliderComponent.html) \
`carve` [CarveComponent](../../Murder/Components/CarveComponent.html) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### TrackEntityOnGrid(Map, Entity, IntRectangle)

```csharp
protected void TrackEntityOnGrid(Map map, Entity e, IntRectangle rect)
```

Marks the cells in `rect` as occupied/carved on the map for the specified entity.

**Parameters** \
`map` [Map](../../Murder/Core/Map.html) \
`e` [Entity](../../Bang/Entities/Entity.html) \
`rect` [IntRectangle](../../Murder/Core/Geometry/IntRectangle.html) \

#### UntrackEntityOnGrid(Map, Entity, IntRectangle, bool)

```csharp
protected void UntrackEntityOnGrid(Map map, Entity e, IntRectangle rect, bool force)
```

Removes the entity's carve from the map cells; set `force` to bypass the guard that prevents accidental double-removal.

**Parameters** \
`map` [Map](../../Murder/Core/Map.html) \
`e` [Entity](../../Bang/Entities/Entity.html) \
`rect` [IntRectangle](../../Murder/Core/Geometry/IntRectangle.html) \
`force` [bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

```csharp
public virtual void OnAdded(World world, ImmutableArray<T> entities)
```

Carves the initial bounding boxes of newly added entities into the map grid and refreshes the pathfinding data.

**Parameters** \
`world` [World](../../Bang/World.html) \
`entities` [ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \

```csharp
public virtual void OnModified(World world, ImmutableArray<T> entities)
```

Updates the map grid by removing the previous bounding box and carving the new one whenever a carve entity moves or changes.

**Parameters** \
`world` [World](../../Bang/World.html) \
`entities` [ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \

```csharp
public virtual void OnRemoved(World world, ImmutableArray<T> entities)
```

Restores the cells previously occupied by a removed carve entity and refreshes the pathfinding data.

**Parameters** \
`world` [World](../../Bang/World.html) \
`entities` [ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \

#### OnActivated(World, ImmutableArray<T>)

```csharp
public virtual void OnActivated(World world, ImmutableArray<T> entities)
```

Re-carves reactivated entities exactly like a fresh add, by delegating straight to `OnAdded`.

**Parameters** \
`world` [World](../../Bang/World.html) \
`entities` [ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \

#### OnDeactivated(World, ImmutableArray<T>)

```csharp
public virtual void OnDeactivated(World world, ImmutableArray<T> entities)
```

Un-carves deactivated entities exactly like a removal, by delegating straight to `OnRemoved`, so a deactivated obstacle temporarily stops blocking pathfinding.

**Parameters** \
`world` [World](../../Bang/World.html) \
`entities` [ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \

⚡
