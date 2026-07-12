# CollisionLayersBase

**Namespace:** Murder.Core.Physics \
**Assembly:** Murder.dll

```csharp
public class CollisionLayersBase
```

Registry of the built-in collision layer bit-constants used throughout the engine (colliders, the map's collision grid, the quadtree, ray/line-of-sight checks, and pathfinding) to categorize what kind of object a bit in a collision mask represents.

**Intent:** Each constant is a single bit so masks can be combined with bitwise OR (e.g. `SOLID | HOLE`) to describe "blocks any of these layers". Game-specific projects are expected to subclass this and add their own layers using the unused higher bits.

**Use-case:** Reference these constants when setting the collision layer/mask on a `ColliderComponent`, building a custom collision or line-of-sight mask, or filtering entities in physics callbacks.

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

Layer for entities that move and interact with the world — players, enemies, and other actors (bit 3).

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

Layer for pit/hole areas that actors fall into or are otherwise affected by when they enter them (bit 4).

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

Layer for tiles that block pathfinding routes but are not necessarily solid to physical movement (bit 8).

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### RAYIGNORE

```csharp
public static const int RAYIGNORE;
```

Layer for entities that should be excluded from ray-cast checks (bit 7).

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
