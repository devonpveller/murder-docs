# QuadtreeCalculatorSystem

**Namespace:** Murder.Systems \
**Assembly:** Murder.dll

```csharp
public class QuadtreeCalculatorSystem : IReactiveSystem, ISystem
```

Maintains a spatial `Quadtree` by inserting, updating, and removing entities with `PositionComponent` and `ColliderComponent` whenever their transform or collider changes.

**Intent:** Keeps the world's spatial index accurate so collision and physics systems can efficiently query nearby entities.

**Use-case:** Required by `TriggerPhysicsSystem` and any other system that performs spatial queries; must be present in any world that uses collision detection.

**Implements:** _[IReactiveSystem](../../Bang/Systems/IReactiveSystem.html), [ISystem](../../Bang/Systems/ISystem.html)_

### ⭐ Constructors
```csharp
public QuadtreeCalculatorSystem()
```

### ⭐ Methods
#### OnActivated(World, ImmutableArray<T>)
```csharp
public virtual void OnActivated(World world, ImmutableArray<T> entities)
```

Re-inserts reactivated entities into the spatial quadtree.

**Parameters** \
`world` [World](../../Bang/World.html) \
`entities` [ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \

#### OnAdded(World, ImmutableArray<T>)
```csharp
public virtual void OnAdded(World world, ImmutableArray<T> entities)
```

Inserts newly added entities into the spatial quadtree.

**Parameters** \
`world` [World](../../Bang/World.html) \
`entities` [ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \

#### OnDeactivated(World, ImmutableArray<T>)
```csharp
public virtual void OnDeactivated(World world, ImmutableArray<T> entities)
```

Removes deactivated entities from the quadtree so they are excluded from spatial queries.

**Parameters** \
`world` [World](../../Bang/World.html) \
`entities` [ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \

#### OnModified(World, ImmutableArray<T>)
```csharp
public virtual void OnModified(World world, ImmutableArray<T> entities)
```

Updates each entity's bounding box entry in the quadtree when its position or collider changes.

**Parameters** \
`world` [World](../../Bang/World.html) \
`entities` [ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \

#### OnRemoved(World, ImmutableArray<T>)
```csharp
public virtual void OnRemoved(World world, ImmutableArray<T> entities)
```

Removes destroyed entities from the quadtree.

**Parameters** \
`world` [World](../../Bang/World.html) \
`entities` [ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \



⚡