# CollisionCacheComponent

**Namespace:** Murder.Components \
**Assembly:** Murder.dll

```csharp
public sealed struct CollisionCacheComponent : IComponent
```

Caches the set of entity IDs that are currently overlapping this entity's collider.

**Implements:** _[IComponent](../../Bang/Components/IComponent.html)_

**Intent:** Provides a fast lookup of which entities are in contact so collision-response systems do not need to re-query the physics world every frame.

**Use-case:** Added and updated automatically by the physics system; query `CollidingWith` to iterate or test for specific colliders, and call `Add`/`Remove` to update it immutably.

### ⭐ Constructors
```csharp
public CollisionCacheComponent()
```

```csharp
public CollisionCacheComponent(ImmutableHashSet<T> idList)
```

**Parameters** \
`idList` [ImmutableHashSet\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableHashSet-1?view=net-7.0) \

```csharp
public CollisionCacheComponent(int id)
```

**Parameters** \
`id` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

### ⭐ Properties
#### CollidingWith
```csharp
public ImmutableHashSet<T> CollidingWith { get; }
```

The set of entity IDs currently overlapping this entity's collider.

**Returns** \
[ImmutableHashSet\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableHashSet-1?view=net-7.0) \
### ⭐ Methods
#### Contains(World)
```csharp
public bool Contains(World world)
```

Returns `true` if any entity in the collision set has a component of type `T`.

**Parameters** \
`world` [World](../../Bang/World.html) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### HasId(int)
```csharp
public bool HasId(int id)
```

Returns `true` if the entity with `id` is in the current collision set.

**Parameters** \
`id` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### Add(int)
```csharp
public CollisionCacheComponent Add(int id)
```

Returns a new component with `id` added to the collision set.

**Parameters** \
`id` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

**Returns** \
[CollisionCacheComponent](../../Murder/Components/CollisionCacheComponent.html) \

#### Remove(int)
```csharp
public CollisionCacheComponent Remove(int id)
```

Returns a new component with `id` removed from the collision set.

**Parameters** \
`id` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

**Returns** \
[CollisionCacheComponent](../../Murder/Components/CollisionCacheComponent.html) \

#### GetCollidingEntities(World)
```csharp
public IEnumerable<T> GetCollidingEntities(World world)
```

Enumerates all live entities currently in the collision set.

**Parameters** \
`world` [World](../../Bang/World.html) \

**Returns** \
[IEnumerable\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Generic.IEnumerable-1?view=net-7.0) \



⚡