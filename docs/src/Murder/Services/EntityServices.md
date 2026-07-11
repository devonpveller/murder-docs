# EntityServices

**Namespace:** Murder.Services \
**Assembly:** Murder.dll

```csharp
public static class EntityServices
```

General-purpose ECS entity utilities for animation playback, hierarchy traversal, spawning, and component helpers.

**Intent:** Provides convenience methods that operate on entities but don't belong to a more specific service domain.

**Use-case:** Use to play sprite animations, rotate entity positions, spawn prefab clusters, subscribe to animation events, or look up entity metadata without writing boilerplate component queries.

### ⭐ Methods
#### AnimationAvailable(Entity, string)
```csharp
public bool AnimationAvailable(Entity entity, string id)
```
Returns `true` if the entity's sprite asset contains an animation with the given identifier.

**Parameters** \
`entity` [Entity](../../Bang/Entities/Entity.html) \
`id` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### IsChildOf(World, Entity, Entity)
```csharp
public bool IsChildOf(World world, Entity parent, Entity child)
```
Returns `true` if `child` is a direct child of `parent`.

**Parameters** \
`world` [World](../../Bang/World.html) \
`parent` [Entity](../../Bang/Entities/Entity.html) \
`child` [Entity](../../Bang/Entities/Entity.html) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### IsInCamera(Entity, World)
```csharp
public bool IsInCamera(Entity e, World world)
```
Returns `true` if the entity's position falls within the current camera viewport.

**Parameters** \
`e` [Entity](../../Bang/Entities/Entity.html) \
`world` [World](../../Bang/World.html) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### FindRootEntity(Entity)
```csharp
public Entity FindRootEntity(Entity e)
```
Traverses the parent chain and returns the topmost ancestor entity (the root).

**Parameters** \
`e` [Entity](../../Bang/Entities/Entity.html) \

**Returns** \
[Entity](../../Bang/Entities/Entity.html) \

#### TryFindTarget(Entity, World, string)
```csharp
public Entity TryFindTarget(Entity entity, World world, string name)
```

Try to find the target of a [GuidToIdTargetCollectionComponent](../../Murder/Components/GuidToIdTargetCollectionComponent.html).

**Parameters** \
`entity` [Entity](../../Bang/Entities/Entity.html) \
`world` [World](../../Bang/World.html) \
`name` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

**Returns** \
[Entity](../../Bang/Entities/Entity.html) \

#### TryFindTarget(Entity, World)
```csharp
public Entity TryFindTarget(Entity entity, World world)
```

Try to find the target of a [GuidToIdTargetComponent](../../Murder/Components/GuidToIdTargetComponent.html).

**Parameters** \
`entity` [Entity](../../Bang/Entities/Entity.html) \
`world` [World](../../Bang/World.html) \

**Returns** \
[Entity](../../Bang/Entities/Entity.html) \

#### FindAllTargets(Entity, string)
```csharp
public IEnumerable<T> FindAllTargets(Entity e, string prefix)
```

Return all targets of entity that start with <paramref name="prefix" />.
            This will first check for a target id. If none, it will check for a target
            collection with <paramref name="prefix" />.

**Parameters** \
`e` [Entity](../../Bang/Entities/Entity.html) \
`prefix` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

**Returns** \
[IEnumerable\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Generic.IEnumerable-1?view=net-7.0) \

#### TryActiveSpriteAsset(Entity)
```csharp
public SpriteAsset TryActiveSpriteAsset(Entity entity)
```
Returns the `SpriteAsset` referenced by the entity's sprite component, or `null` if it has none.

**Parameters** \
`entity` [Entity](../../Bang/Entities/Entity.html) \

**Returns** \
[SpriteAsset](../../Murder/Assets/Graphics/SpriteAsset.html) \

#### TryGetEntityName(Entity)
```csharp
public string TryGetEntityName(Entity entity)
```
Returns the debug or designer name assigned to the entity, or `null` if none is set.

**Parameters** \
`entity` [Entity](../../Bang/Entities/Entity.html) \

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### PlayAsepriteAnimationNext(Entity, string)
```csharp
public T? PlayAsepriteAnimationNext(Entity entity, string animationName)
```
Queues the named animation to play immediately after the current one finishes.

**Parameters** \
`entity` [Entity](../../Bang/Entities/Entity.html) \
`animationName` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

**Returns** \
[T?](https://learn.microsoft.com/en-us/dotnet/api/System.Nullable-1?view=net-7.0) \

#### PlaySpriteAnimation(Entity, ImmutableArray<T>)
```csharp
public T? PlaySpriteAnimation(Entity entity, ImmutableArray<T> animations)
```

Plays an animation or animation sequence. Loops the last animation.

**Parameters** \
`entity` [Entity](../../Bang/Entities/Entity.html) \
\
`animations` [ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \
\

**Returns** \
[T?](https://learn.microsoft.com/en-us/dotnet/api/System.Nullable-1?view=net-7.0) \
\

#### PlaySpriteAnimation(Entity, String[])
```csharp
public T? PlaySpriteAnimation(Entity entity, String[] nextAnimations)
```

Plays an animation or animation sequence. Loops the last animation.

**Parameters** \
`entity` [Entity](../../Bang/Entities/Entity.html) \
\
`nextAnimations` [string[]](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
\

**Returns** \
[T?](https://learn.microsoft.com/en-us/dotnet/api/System.Nullable-1?view=net-7.0) \
\

#### PlaySpriteAnimationOnce(Entity, string)
```csharp
public T? PlaySpriteAnimationOnce(Entity entity, string animation)
```

Plays an animation or animation sequence. Do not loop.

**Parameters** \
`entity` [Entity](../../Bang/Entities/Entity.html) \
\
`animation` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
\

**Returns** \
[T?](https://learn.microsoft.com/en-us/dotnet/api/System.Nullable-1?view=net-7.0) \
\

#### TryPlayAsepriteAnimationNext(Entity, string)
```csharp
public T? TryPlayAsepriteAnimationNext(Entity entity, string animationName)
```
Attempts to queue the named animation after the current one; returns `null` if the entity has no sprite or the animation is unavailable.

**Parameters** \
`entity` [Entity](../../Bang/Entities/Entity.html) \
`animationName` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

**Returns** \
[T?](https://learn.microsoft.com/en-us/dotnet/api/System.Nullable-1?view=net-7.0) \

#### TryPlaySpriteAnimation(Entity, ImmutableArray<T>)
```csharp
public T? TryPlaySpriteAnimation(Entity entity, ImmutableArray<T> nextAnimations)
```
Attempts to play an animation sequence; returns `null` silently if the entity has no sprite component.

**Parameters** \
`entity` [Entity](../../Bang/Entities/Entity.html) \
`nextAnimations` [ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \

**Returns** \
[T?](https://learn.microsoft.com/en-us/dotnet/api/System.Nullable-1?view=net-7.0) \

#### TryPlaySpriteAnimation(Entity, String[])
```csharp
public T? TryPlaySpriteAnimation(Entity entity, String[] nextAnimations)
```
Attempts to play an animation sequence from a string array; returns `null` silently if the entity has no sprite component.

**Parameters** \
`entity` [Entity](../../Bang/Entities/Entity.html) \
`nextAnimations` [string[]](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

**Returns** \
[T?](https://learn.microsoft.com/en-us/dotnet/api/System.Nullable-1?view=net-7.0) \

#### RemoveSpeedMultiplier(Entity, int)
```csharp
public void RemoveSpeedMultiplier(Entity entity, int slot)
```
Removes the speed multiplier occupying the given slot from the entity's `AgentSpeedMultiplierComponent`.

**Parameters** \
`entity` [Entity](../../Bang/Entities/Entity.html) \
`slot` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### RotateChildPositions(World, Entity, float)
```csharp
public void RotateChildPositions(World world, Entity entity, float angle)
```
Rotates the world positions of all child entities around the parent entity's position by `angle` radians.

**Parameters** \
`world` [World](../../Bang/World.html) \
`entity` [Entity](../../Bang/Entities/Entity.html) \
`angle` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### RotatePosition(Entity, float)
```csharp
public void RotatePosition(Entity entity, float angle)
```
Rotates the entity's position by `angle` radians around the origin.

**Parameters** \
`entity` [Entity](../../Bang/Entities/Entity.html) \
`angle` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### RotatePositionAround(Entity, Vector2, float)
```csharp
public void RotatePositionAround(Entity entity, Vector2 center, float angle)
```
Rotates the entity's world position by `angle` radians around `center`.

**Parameters** \
`entity` [Entity](../../Bang/Entities/Entity.html) \
`center` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`angle` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### SetAgentSpeedMultiplier(Entity, int, float)
```csharp
public void SetAgentSpeedMultiplier(Entity entity, int slot, float speedMultiplier)
```
Sets a speed multiplier for the agent in the given slot, used to additively adjust movement speed.

**Parameters** \
`entity` [Entity](../../Bang/Entities/Entity.html) \
`slot` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`speedMultiplier` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### Spawn(World, Vector2, Guid, int, float, IComponent[])
```csharp
public void Spawn(World world, Vector2 spawnerPosition, Guid entityToSpawn, int count, float radius, IComponent[] addComponents)
```
Spawns `count` copies of the given prefab scattered within `radius` of `spawnerPosition`, each with optional extra components.

**Parameters** \
`world` [World](../../Bang/World.html) \
`spawnerPosition` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`entityToSpawn` [Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \
`count` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`radius` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`addComponents` [IComponent[]](../../Bang/Components/IComponent.html) \

#### SubscribeToAnimationEvents(Entity, Entity)
```csharp
public void SubscribeToAnimationEvents(Entity listener, Entity broadcaster)
```
Merges the animation event listeners of `broadcaster` into `listener` so that `listener` receives `broadcaster`'s animation events.

**Parameters** \
`listener` [Entity](../../Bang/Entities/Entity.html) \
`broadcaster` [Entity](../../Bang/Entities/Entity.html) \



⚡