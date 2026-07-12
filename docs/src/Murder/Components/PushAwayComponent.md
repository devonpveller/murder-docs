# PushAwayComponent

**Namespace:** Murder.Components \
**Assembly:** Murder.dll

```csharp
public sealed struct PushAwayComponent : IComponent
```

Marks an entity as a source of a soft "push away" area: nearby entities that also carry a collider are nudged out of this square region every frame.

**Intent:** Provide a cheap, broad-phase repulsion effect for keeping crowds of entities from overlapping, separate from hard physical collision resolution.

**Use-case:** Attach to agents, obstacles, or crowd entities that should gently shove nearby colliding entities away from them (e.g. NPCs milling around a market stall). Unlike [ColliderComponent](../../Murder/Components/ColliderComponent.html), which produces hard collisions resolved by `SATPhysicsSystem`, this component is indexed into the world's `Quadtree.PushAway` spatial tree by `QuadtreeCalculatorSystem` and evaluated as a soft repulsion, so it's much cheaper for large numbers of entities.

**Implements:** _[IComponent](../../Bang/Components/IComponent.html)_

### ⭐ Constructors

```csharp
public PushAwayComponent(int size, int strength)
```

Creates a push-away area with the given side length and repulsion strength.

**Parameters** \
`size` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`strength` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

### ⭐ Properties

#### Size

```csharp
public readonly float Size;
```

Side length, in pixels, of the square area centered on the entity's position within which other entities are pushed away.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### Strength

```csharp
public readonly float Strength;
```

How forcefully entities inside the push-away area are repelled; a larger value produces a stronger shove.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

### ⭐ Methods

#### GetBoundingBox(PositionComponent)

```csharp
public Rectangle GetBoundingBox(PositionComponent position)
```

Returns the square push-away bounding box centered on `position`'s coordinates. Used when indexing this component into the world's push-away quadtree.

**Parameters** \
`position` [PositionComponent](../../Bang/Components/PositionComponent.html) \

**Returns** \
[Rectangle](../../Murder/Core/Geometry/Rectangle.html) \

#### GetBoundingBox(Vector2)

```csharp
public Rectangle GetBoundingBox(Vector2 position)
```

Returns the square push-away bounding box centered on the given world-space position.

**Parameters** \
`position` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

**Returns** \
[Rectangle](../../Murder/Core/Geometry/Rectangle.html) \

⚡
