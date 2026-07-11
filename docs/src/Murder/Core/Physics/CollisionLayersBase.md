# CollisionLayersBase

**Namespace:** Murder.Core.Physics \
**Assembly:** Murder.dll

```csharp
public class CollisionLayersBase
```

Base class that defines the built-in collision layer bit-constants used by the `Map` and quadtree systems to categorize collidable entities.

**Intent:** Registry of named bitmask constants that identify the role of a collidable object (actor, solid wall, trigger, hitbox, etc.).

**Use-case:** Reference these constants when setting the collision layer on a `ColliderComponent`, querying `Map.HasCollision`, or filtering entities in physics callbacks.

### ⭐ Constructors
```csharp
protected CollisionLayersBase()
```

This class should never be instanced

### ⭐ Properties
#### ACTOR
```csharp
public static const int ACTOR;
```

Layer for entities that move and interact with the world (bit 3).

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
#### BLOCK_VISION
```csharp
public static const int BLOCK_VISION;
```

Layer for entities or tiles that block line-of-sight checks (bit 6).

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
#### CARVE
```csharp
public static const int CARVE;
```

Layer for dynamic carve components that cut holes into the navigation/collision map (bit 5).

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
#### HITBOX
```csharp
public static const int HITBOX;
```

Layer for attack hitboxes that deal damage but do not block movement (bit 2).

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
#### HOLE
```csharp
public static const int HOLE;
```

Layer for pit or hole areas that destroy or transition actors that enter them (bit 4).

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
#### NONE
```csharp
public static const int NONE;
```

Empty collision layer (0); no collision.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
#### PATHFIND
```csharp
public static const int PATHFIND;
```

Layer for tiles that block pathfinding but not necessarily physical movement (bit 8).

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
#### RAYIGNORE
```csharp
public static const int RAYIGNORE;
```

Layer for entities that are excluded from ray-cast checks (bit 7).

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
#### RESERVED
```csharp
public static const int RESERVED;
```

A reserved layer bit for game-specific use, not assigned a built-in meaning.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
#### SOLID
```csharp
public static const int SOLID;
```

Layer for fully solid tiles and walls that block all movement (bit 0).

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
#### TRIGGER
```csharp
public static const int TRIGGER;
```

Layer for trigger volumes that fire interactions when an actor overlaps them (bit 1).

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \


⚡