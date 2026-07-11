# Quadtree

**Namespace:** Murder.Core.Physics \
**Assembly:** Murder.dll

```csharp
public class Quadtree
```

Top-level spatial index that maintains three separate `QTNode<T>` trees for collision, push-away, and static rendering queries.

**Intent:** The engine's primary broad-phase spatial acceleration structure for fast overlap and proximity queries.

**Use-case:** Retrieved via `Quadtree.GetOrCreateUnique(world)` in physics systems; add entities with `AddToCollisionQuadTree` and query with `GetCollisionEntitiesAt` to find potential collision candidates.

### ⭐ Constructors
```csharp
public Quadtree(Rectangle mapBounds)
```

Creates a `Quadtree` that covers the given world-space `mapBounds` rectangle.

**Parameters** \
`mapBounds` [Rectangle](../../../Murder/Core/Geometry/Rectangle.html) \

### ⭐ Properties
#### Collision
```csharp
public readonly QTNode<T> Collision;
```

The quadtree partition containing all entities registered for collision queries.

**Returns** \
[QTNode\<T\>](../../../Murder/Core/Physics/QTNode-1.html) \
#### PushAway
```csharp
public readonly QTNode<T> PushAway;
```

The quadtree partition containing entities that push other actors away (solid body separation).

**Returns** \
[QTNode\<T\>](../../../Murder/Core/Physics/QTNode-1.html) \
#### StaticRender
```csharp
public readonly QTNode<T> StaticRender;
```

The quadtree partition containing static entities used for render-culling queries.

**Returns** \
[QTNode\<T\>](../../../Murder/Core/Physics/QTNode-1.html) \
### ⭐ Methods
#### GetOrCreateUnique(World)
```csharp
public Quadtree GetOrCreateUnique(World world)
```

Retrieves the singleton `Quadtree` stored in the world, creating it if it does not exist.

**Parameters** \
`world` [World](../../../Bang/World.html) \

**Returns** \
[Quadtree](../../../Murder/Core/Physics/Quadtree.html) \

#### AddToCollisionQuadTree(IEnumerable<T>)
```csharp
public void AddToCollisionQuadTree(IEnumerable<T> entities)
```

Inserts the given entities into the collision quadtree partition.

**Parameters** \
`entities` [IEnumerable\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Generic.IEnumerable-1?view=net-7.0) \

#### AddToStaticRenderQuadTree(IEnumerable<T>)
```csharp
public void AddToStaticRenderQuadTree(IEnumerable<T> entities)
```

Inserts the given entities into the static render quadtree partition.

**Parameters** \
`entities` [IEnumerable\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Generic.IEnumerable-1?view=net-7.0) \

#### GetCollisionEntitiesAt(Rectangle, List<T>)
```csharp
public void GetCollisionEntitiesAt(Rectangle boundingBox, List<T> list)
```

Populates `list` with all entities in the collision partition whose bounding box overlaps `boundingBox`.

**Parameters** \
`boundingBox` [Rectangle](../../../Murder/Core/Geometry/Rectangle.html) \
`list` [List\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Generic.List-1?view=net-7.0) \

#### RemoveFromCollisionQuadTree(IEnumerable<T>)
```csharp
public void RemoveFromCollisionQuadTree(IEnumerable<T> entities)
```

Removes the given entities from the collision quadtree partition.

**Parameters** \
`entities` [IEnumerable\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Generic.IEnumerable-1?view=net-7.0) \

#### RemoveFromStaticRenderQuadTree(IEnumerable<T>)
```csharp
public void RemoveFromStaticRenderQuadTree(IEnumerable<T> entities)
```

Removes the given entities from the static render quadtree partition.

**Parameters** \
`entities` [IEnumerable\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Generic.IEnumerable-1?view=net-7.0) \

#### UpdateQuadTree(IEnumerable<T>)
```csharp
public void UpdateQuadTree(IEnumerable<T> entities)
```

Completelly clears and rebuilds the quad tree and pushAway quad tree using a given list of entities
            We should avoid this if possible

**Parameters** \
`entities` [IEnumerable\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Generic.IEnumerable-1?view=net-7.0) \
\



⚡