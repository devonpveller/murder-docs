# EntityServices

**Namespace:** Murder.Services \
**Assembly:** Murder.dll

```csharp
public static class EntityServices
```

General-purpose ECS entity utilities for sprite-animation playback, facing/rotation, hierarchy traversal, target lookup, spawning, and small per-component convenience toggles.

**Intent:** Provides convenience methods that operate on entities but don't belong to a more specific service domain (collision, sound, dialogue, etc.). Most of these are extension methods on `Entity`, so they read naturally as `entity.DoThing(...)` at call sites throughout systems and interactions.

**Use-case:** Use to play/queue sprite animations without manually touching `SpriteComponent` (`PlaySpriteAnimation`, `TryPlaySpriteAnimation`, `PlaySpriteAnimationNext`, `PlaySpriteAnimationOnce`, `PlayOrContinueAnimation`, `PlayAnimationOverload`), rotate or reface entities (`TurnFaceTowards`, `RotatePosition`, `RotatePositionAround`, `RotateChildPositions`), walk or query the parent/child hierarchy (`FindRootEntity`, `IsChildOf`), resolve `IdTarget`/`IdTargetCollection` references (`TryFindTarget`, `FindTarget`, `FetchTarget`, `FindAllTargets`), spawn prefab clusters (`Spawn`), or toggle small per-entity states like disabled/paused agents and speed multipliers.

### ⭐ Methods

#### FetchRequiredChild(Entity, string, string)

```csharp
public static Entity FetchRequiredChild(Entity e, string name, [CallerMemberName] string? caller = null)
```

Looks up the child of `e` named `name` via `TryFetchChild` and throws an `InvalidStateMachineException` (naming the calling member) if it isn't found. Use this instead of `TryFetchChild` when a child is a hard structural requirement (e.g. a state machine expects a specific named part to exist) and its absence should fail loudly rather than be silently tolerated.

**Parameters** \
`e` [Entity](../../Bang/Entities/Entity.html) \
`name` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
`caller` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

**Returns** \
[Entity](../../Bang/Entities/Entity.html) \

#### TurnFaceTowards(Entity, Entity, float)

```csharp
public static void TurnFaceTowards(this Entity entity, Entity otherEntity, float duration)
```

Computes the `Direction` from `entity` to `otherEntity` (via `DirectionHelper.LookAtEntity`) and starts turning `entity` to face it over `duration` seconds. Use this for agents that should visually orient toward another entity (dialogue partner, target, threat) rather than snapping instantly.

**Parameters** \
`entity` [Entity](../../Bang/Entities/Entity.html) \
`otherEntity` [Entity](../../Bang/Entities/Entity.html) \
`duration` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### TurnFaceTowards(Entity, Vector2, float)

```csharp
public static void TurnFaceTowards(this Entity entity, Vector2 goal, float duration)
```

Computes the `Direction` from `entity` toward world position `goal` (via `DirectionHelper.LookAtPosition`) and starts turning to face it over `duration` seconds. Use this when the target isn't an entity (e.g. facing toward a clicked point or a waypoint).

**Parameters** \
`entity` [Entity](../../Bang/Entities/Entity.html) \
`goal` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`duration` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### TurnFaceTowards(Entity, Direction, float)

```csharp
public static void TurnFaceTowards(this Entity entity, Direction targetDirection, float duration)
```

Turns `entity` from its current facing (or `Direction.Up` if unset) toward `targetDirection`. If already facing that direction this is a no-op; if `duration` is `0` the facing is set immediately via `SetFacing`, otherwise a timed `FacingTurn` (interpolated between `Game.Now` and `Game.Now + duration`) is started so the turn animates.

**Parameters** \
`entity` [Entity](../../Bang/Entities/Entity.html) \
`targetDirection` [Direction](../../Murder/Helpers/Direction.html) \
`duration` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### TurnFaceTowards(Entity, Direction, Direction, float)

```csharp
public static void TurnFaceTowards(this Entity entity, Direction fromDirection, Direction targetDirection, float duration)
```

Forces `entity`'s current facing to `fromDirection` first (via `SetFacing`), then starts a timed turn toward `targetDirection` over `duration` seconds. Use this when the starting facing needs to be pinned explicitly rather than inferred from the entity's existing state — e.g. scripted sequences that need a deterministic turn animation.

**Parameters** \
`entity` [Entity](../../Bang/Entities/Entity.html) \
`fromDirection` [Direction](../../Murder/Helpers/Direction.html) \
`targetDirection` [Direction](../../Murder/Helpers/Direction.html) \
`duration` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### IsMoving(Entity)

```csharp
public static bool IsMoving(Entity e)
```

Returns `true` if `e` has any of `VelocityComponent`, `AgentImpulseComponent`, `MoveToComponent`, `PathfindComponent`, or `MoveToPerfectComponent` — i.e. any indication it's currently walking toward something. The remarks in source note this deliberately doesn't rely on impulse alone, since impulse can be momentarily zero mid-movement.

**Parameters** \
`e` [Entity](../../Bang/Entities/Entity.html) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### FetchScale(Entity)

```csharp
public static Vector2 FetchScale(this Entity entity)
```

Returns the entity's `ScaleComponent.Scale`, or `Vector2.One` if it has none. Use this instead of manually checking for a `ScaleComponent` whenever you need an entity's effective scale with a safe default.

**Parameters** \
`entity` [Entity](../../Bang/Entities/Entity.html) \

**Returns** \
[Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

#### GetGlobalPositionIfValid(Entity)

```csharp
public static Vector2? GetGlobalPositionIfValid(this Entity? entity)
```

Returns `entity.GetGlobalPosition()`, or `null` if `entity` is `null`, inactive, destroyed, or lacks a `PositionComponent`. Use this in code paths that hold onto an entity reference across frames and need a defensive, allocation-free way to check "is this still a valid, positioned entity?" before using its position.

**Parameters** \
`entity` [Entity](../../Bang/Entities/Entity.html) \

**Returns** \
[Vector2?](https://learn.microsoft.com/en-us/dotnet/api/System.Nullable-1?view=net-7.0) \

#### SubscribeToAnimationEvents(Entity, Entity)

```csharp
public static void SubscribeToAnimationEvents(this Entity listener, Entity broadcaster)
```

Adds `listener`'s entity id to `broadcaster`'s `AnimationEventBroadcasterComponent` subscriber list (creating the component if `broadcaster` doesn't have one). Once subscribed, `listener` receives animation events fired by `broadcaster`'s sprite — used to let a child/related entity react to a parent's animation cues (e.g. spawn a footstep effect on a specific frame of a walk animation).

**Parameters** \
`listener` [Entity](../../Bang/Entities/Entity.html) \
`broadcaster` [Entity](../../Bang/Entities/Entity.html) \

#### RotateChildPositions(World, Entity, float)

```csharp
public static void RotateChildPositions(World world, Entity entity, float angle)
```

Rotates the local position of every direct child of `entity` by `angle` radians around the origin. Use this to spin a composite entity's parts together (e.g. rotating limbs, orbiting satellites) without moving `entity` itself.

**Parameters** \
`world` [World](../../Bang/World.html) \
`entity` [Entity](../../Bang/Entities/Entity.html) \
`angle` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### RotatePositionAround(Entity, Vector2, float)

```csharp
public static void RotatePositionAround(Entity entity, Vector2 center, float angle)
```

Rotates `entity`'s position by `angle` radians around the world point `center`, rather than around the origin. Use this for orbiting behavior or rotating an entity as part of a group pivoting around a shared point.

**Parameters** \
`entity` [Entity](../../Bang/Entities/Entity.html) \
`center` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`angle` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### RotatePosition(Entity, float)

```csharp
public static void RotatePosition(Entity entity, float angle)
```

Rotates `entity`'s local position by `angle` radians around the coordinate origin.

**Parameters** \
`entity` [Entity](../../Bang/Entities/Entity.html) \
`angle` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### IsChildOf(World, Entity, Entity)

```csharp
public static bool IsChildOf(World world, Entity parent, Entity child)
```

Returns `true` if `child` is `parent`, walking up `child`'s parent chain (recursively resolving each `Parent` id through `world`) until `parent` is found or the chain ends. Unlike a simple direct-parent check, this correctly answers "is child anywhere underneath parent in the hierarchy?"

**Parameters** \
`world` [World](../../Bang/World.html) \
`parent` [Entity](../../Bang/Entities/Entity.html) \
`child` [Entity](../../Bang/Entities/Entity.html) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### FindRootEntity(Entity)

```csharp
public static Entity FindRootEntity(Entity e)
```

Recursively follows `e.Parent`/`TryFetchParent` up the hierarchy and returns the topmost ancestor (or `e` itself if it has no parent). Used throughout the engine (e.g. `EffectsServices.ApplyHighlight`) whenever an effect or query needs to operate on the "whole object" rather than a sub-part.

**Parameters** \
`e` [Entity](../../Bang/Entities/Entity.html) \

**Returns** \
[Entity](../../Bang/Entities/Entity.html) \

#### TryPlayAfterWhenDifferent(Entity, string)

```csharp
public static bool TryPlayAfterWhenDifferent(this Entity e, string id)
```

Queues animation `id` to play after the current one *only* if `e`'s sprite isn't already playing or already queued to play `id` next — avoiding redundant re-queuing of an animation that's already active or pending. Returns `false` (and does nothing) if `e` has no `SpriteComponent`, if `id` is already the current animation, or if `id` is already the last queued animation.

**Parameters** \
`e` [Entity](../../Bang/Entities/Entity.html) \
`id` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### PlaySpriteAnimationNext(Entity, string)

```csharp
public static bool PlaySpriteAnimationNext(this Entity entity, string animationName)
```

Queues `animationName` to play after the current animation (via `TryPlayAfterWhenDifferent`) and, if it was actually queued, clears any pending "animation complete" flags/messages so the follow-up animation isn't immediately treated as finished. Returns whether the animation was queued.

**Parameters** \
`entity` [Entity](../../Bang/Entities/Entity.html) \
`animationName` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### PlaySpriteAnimationNext(Entity, string[])

```csharp
public static bool PlaySpriteAnimationNext(this Entity entity, params string[] animations)
```

Overload of `PlaySpriteAnimationNext` that queues a sequence of animations (via `SpriteComponent.PlayAfter`) to play back-to-back after the current one, rather than a single clip. Returns `true` if the entity had a sprite component to update.

**Parameters** \
`entity` [Entity](../../Bang/Entities/Entity.html) \
`animations` [string[]](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### PlaySpriteAnimationNext(Entity, ImmutableArray&lt;string&gt;)

```csharp
public static SpriteComponent? PlaySpriteAnimationNext(this Entity entity, ImmutableArray<string> animations)
```

Same as the `params string[]` overload but takes an `ImmutableArray<string>` directly and returns the updated `SpriteComponent` (or `null` if the entity has no sprite), letting callers inspect the resulting sprite state.

**Parameters** \
`entity` [Entity](../../Bang/Entities/Entity.html) \
`animations` [ImmutableArray\<string\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \

**Returns** \
[SpriteComponent?](../../Murder/Components/SpriteComponent.html) \

#### TryPlaySpriteAnimation(Entity, string[])

```csharp
public static SpriteComponent? TryPlaySpriteAnimation(this Entity entity, params string[] nextAnimations)
```

Convenience overload of `TryPlaySpriteAnimation(Entity, ImmutableArray<string>, Guid?)` that accepts a `params` array. Returns `null` silently (no warning logged) if the entity has no sprite, making it safe to call speculatively.

**Parameters** \
`entity` [Entity](../../Bang/Entities/Entity.html) \
`nextAnimations` [string[]](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

**Returns** \
[SpriteComponent?](../../Murder/Components/SpriteComponent.html) \

#### TryPlaySpriteAnimation(Entity, ImmutableArray&lt;string&gt;, Guid?)

```csharp
public static SpriteComponent? TryPlaySpriteAnimation(this Entity entity, ImmutableArray<string> nextAnimations, Guid? replaceSpriteGuid = null)
```

Plays `nextAnimations` on `entity`'s sprite (looping the last one), clearing any "do not loop"/"animation started"/"animation complete" flags first. If the sprite is already playing exactly this sequence, it's left untouched (no restart) and returned as-is. `replaceSpriteGuid`, if given, swaps the sprite asset used for playback. Returns `null` if the entity has no `SpriteComponent` — this is the "safe", non-asserting counterpart to `PlaySpriteAnimation`.

**Parameters** \
`entity` [Entity](../../Bang/Entities/Entity.html) \
`nextAnimations` [ImmutableArray\<string\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \
`replaceSpriteGuid` [Guid?](https://learn.microsoft.com/en-us/dotnet/api/System.Nullable-1?view=net-7.0) \

**Returns** \
[SpriteComponent?](../../Murder/Components/SpriteComponent.html) \

#### PlayOrContinueAnimation(Entity, string)

```csharp
public static SpriteComponent? PlayOrContinueAnimation(this Entity entity, string animation)
```

Returns the current sprite unchanged if `animation` is already playing; otherwise delegates to `PlaySpriteAnimation` to start it. Use this when you want idempotent "make sure this animation is playing" semantics without restarting an animation that's already running (e.g. re-applying an idle/walk state every frame from a system).

**Parameters** \
`entity` [Entity](../../Bang/Entities/Entity.html) \
`animation` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

**Returns** \
[SpriteComponent?](../../Murder/Components/SpriteComponent.html) \

#### PlaySpriteAnimation(Entity, ImmutableArray&lt;string&gt;, Guid?)

```csharp
public static SpriteComponent? PlaySpriteAnimation(this Entity entity, ImmutableArray<string> nextAnimations, Guid? replaceSpriteGuid = null)
```

Plays an animation or animation sequence, looping the last one, via `TryPlaySpriteAnimation`. Unlike the `Try` variant, this asserts (`GameLogger.Verify`) that the entity actually has a sprite component, so use this when a missing sprite indicates a real bug rather than an expected case.

**Parameters** \
`entity` [Entity](../../Bang/Entities/Entity.html) \
`nextAnimations` [ImmutableArray\<string\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \
`replaceSpriteGuid` [Guid?](https://learn.microsoft.com/en-us/dotnet/api/System.Nullable-1?view=net-7.0) \

**Returns** \
[SpriteComponent?](../../Murder/Components/SpriteComponent.html) \

#### PlaySpriteAnimationWithOffsetAndBatch(Entity, string, int, int)

```csharp
public static void PlaySpriteAnimationWithOffsetAndBatch(this Entity entity, string animation, int sortOffset, int batch)
```

Plays `animation` (looping) and additionally sets the sprite's sort offset and render batch, in one call. Use this when an ad-hoc animation needs to render in a different batch/order than the entity's usual sprite (e.g. a temporary overlay effect).

**Parameters** \
`entity` [Entity](../../Bang/Entities/Entity.html) \
`animation` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
`sortOffset` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`batch` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### PlaySpriteAnimationWithOffset(Entity, string, int)

```csharp
public static void PlaySpriteAnimationWithOffset(this Entity entity, string animation, int sortOffset)
```

Plays `animation` (looping) with a custom sort offset, without changing the render batch.

**Parameters** \
`entity` [Entity](../../Bang/Entities/Entity.html) \
`animation` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
`sortOffset` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### PlaySpriteAnimationWithOffset(Entity, int, string[])

```csharp
public static void PlaySpriteAnimationWithOffset(this Entity entity, int sortOffset, params string[] nextAnimations)
```

Same as the single-animation overload but accepts a sequence of animation names to play back-to-back, all rendered with `sortOffset`.

**Parameters** \
`entity` [Entity](../../Bang/Entities/Entity.html) \
`sortOffset` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`nextAnimations` [string[]](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### PlaySpriteAnimation(Entity, string[])

```csharp
public static SpriteComponent? PlaySpriteAnimation(this Entity entity, params string[] nextAnimations)
```

`params`-array convenience overload of `PlaySpriteAnimation(Entity, ImmutableArray<string>, Guid?)`; plays an animation or sequence, looping the last one, and asserts the entity has a sprite component.

**Parameters** \
`entity` [Entity](../../Bang/Entities/Entity.html) \
`nextAnimations` [string[]](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

**Returns** \
[SpriteComponent?](../../Murder/Components/SpriteComponent.html) \

#### RestartSpriteAnimation(Entity)

```csharp
public static void RestartSpriteAnimation(this Entity entity)
```

Resets the entity's animation-started timestamp to the current game time, causing the currently playing animation to restart from its first frame without changing which animation is playing.

**Parameters** \
`entity` [Entity](../../Bang/Entities/Entity.html) \

#### AnimationAvailable(Entity, string)

```csharp
public static bool AnimationAvailable(this Entity entity, string id)
```

Returns `true` if the sprite asset referenced by the entity's `AgentSpriteComponent` or `SpriteComponent` contains an animation named `id`. For agent sprites, it additionally checks direction-suffixed variants (e.g. `id_right`) derived from the entity's current facing angle, since directional agents often split one logical animation into per-direction clips.

**Parameters** \
`entity` [Entity](../../Bang/Entities/Entity.html) \
`id` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### TryActiveSpriteAsset(Entity)

```csharp
public static SpriteAsset? TryActiveSpriteAsset(this Entity entity)
```

Returns the `SpriteAsset` referenced by the entity's `AgentSpriteComponent` if present, otherwise its `SpriteComponent`'s asset, or `null` if it has neither (or the referenced asset can't be resolved). Use this when you need to inspect sprite metadata (animation list, frame size, etc.) without caring which of the two sprite component kinds the entity uses.

**Parameters** \
`entity` [Entity](../../Bang/Entities/Entity.html) \

**Returns** \
[SpriteAsset](../../Murder/Assets/Graphics/SpriteAsset.html) \

#### Spawn(World, Vector2, Guid, int, float, IComponent[])

```csharp
public static void Spawn(World world, Vector2 spawnerPosition, Guid entityToSpawn, int count, float radius, params IComponent[] addComponents)
```

Spawns `count` instances of the prefab identified by `entityToSpawn` (via `AssetServices.TryCreate`), scattering each around `spawnerPosition` within `radius` (using `PhysicsServices.FindNextAvailablePosition` to avoid `SOLID`/`HOLE`/`ACTOR` overlap when possible), and attaches every component in `addComponents` to each spawned instance. Use this for spawner-style gameplay (enemy waves, pickups, particles) where you want several copies placed without overlapping obstacles.

**Parameters** \
`world` [World](../../Bang/World.html) \
`spawnerPosition` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`entityToSpawn` [Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \
`count` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`radius` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`addComponents` [IComponent[]](../../Bang/Components/IComponent.html) \

#### PlaySpriteAnimationOnce(Entity, string)

```csharp
public static SpriteComponent? PlaySpriteAnimationOnce(this Entity entity, string animation)
```

Plays `animation` once (not looped) by setting `entity.SetDoNotLoop()` after starting playback, clearing any pending completion flags/messages first. Logs an error and returns `null` if the entity has no `SpriteComponent`. Use this for animations that should play through exactly once (an attack swing, a one-shot reaction) rather than the default looping behavior of the other `PlaySpriteAnimation*` helpers.

**Parameters** \
`entity` [Entity](../../Bang/Entities/Entity.html) \
`animation` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

**Returns** \
[SpriteComponent?](../../Murder/Components/SpriteComponent.html) \

#### TryFindTarget(Entity, World)

```csharp
public static Entity? TryFindTarget(this Entity entity, World world)
```

Resolves the target referenced by the entity's `GuidToIdTargetComponent` (its `IdTarget`), or returns `null` if the entity has no such component or the referenced entity id no longer exists in `world`.

**Parameters** \
`entity` [Entity](../../Bang/Entities/Entity.html) \
`world` [World](../../Bang/World.html) \

**Returns** \
[Entity](../../Bang/Entities/Entity.html) \

#### TryFindTarget(Entity, World, string)

```csharp
public static Entity? TryFindTarget(this Entity entity, World world, string name)
```

Resolves a specific named target from the entity's `GuidToIdTargetCollectionComponent`, or returns `null` if the entity has no such component, `name` isn't in the collection, or the target id no longer exists in `world`. Use this over the single-target overload when an entity can reference multiple named targets (e.g. multiple spawn points or waypoints).

**Parameters** \
`entity` [Entity](../../Bang/Entities/Entity.html) \
`world` [World](../../Bang/World.html) \
`name` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

**Returns** \
[Entity](../../Bang/Entities/Entity.html) \

#### FindAllTargets(Entity, string)

```csharp
public static IEnumerable<int> FindAllTargets(this Entity e, string prefix)
```

Yields every target entity id referenced by `e` whose lookup key starts with `prefix` (case-insensitive): first the single `IdTarget` if present, then every entry in `IdTargetCollection` whose key matches. Use this to gather a whole family of related targets (e.g. all targets whose name begins with `"waypoint_"`) in one pass.

**Parameters** \
`e` [Entity](../../Bang/Entities/Entity.html) \
`prefix` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

**Returns** \
[IEnumerable\<int\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Generic.IEnumerable-1?view=net-7.0) \

#### IsInCamera(Entity, World)

```csharp
public static bool IsInCamera(this Entity e, World world)
```

Returns `true` if `e` has no `PositionComponent` (treated as "everywhere", so it's never culled) or if its global position falls within the current `MonoWorld.Camera.Bounds`. Use this as a cheap visibility/culling check before doing expensive per-frame work on off-screen entities.

**Parameters** \
`e` [Entity](../../Bang/Entities/Entity.html) \
`world` [World](../../Bang/World.html) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### RemoveSpeedMultiplier(Entity, int)

```csharp
public static void RemoveSpeedMultiplier(Entity entity, int slot)
```

Resets the speed multiplier in `slot` back to `1` (no effect) by delegating to `SetAgentSpeedMultiplier`. Use this to clear a previously applied slowdown/speedup (e.g. from a status effect wearing off) without touching multipliers held in other slots.

**Parameters** \
`entity` [Entity](../../Bang/Entities/Entity.html) \
`slot` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### SetAgentSpeedMultiplier(Entity, int, float)

```csharp
public static void SetAgentSpeedMultiplier(Entity entity, int slot, float speedMultiplier)
```

Sets the agent's speed multiplier for the given `slot` on its `AgentSpeedMultiplierComponent` (creating the component if needed). Multiple independent slots let different systems (status effects, terrain, abilities) each apply their own multiplicative speed modifier without overwriting each other; the effective speed is the product of all active slots.

**Parameters** \
`entity` [Entity](../../Bang/Entities/Entity.html) \
`slot` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`speedMultiplier` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### TryGetEntityName(Entity)

```csharp
public static string? TryGetEntityName(Entity entity)
```

Returns the `Name` of the `PrefabAsset` referenced by the entity's `PrefabRefComponent`, or `null` if the entity has no such component or the asset can't be resolved. Use this for debug labeling, logs, or editor display of "what prefab was this entity created from?"

**Parameters** \
`entity` [Entity](../../Bang/Entities/Entity.html) \

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### FindTarget(Entity, string)

```csharp
public static int? FindTarget(this Entity e, string name)
```

Returns the entity id referenced by name `name`: first checked against `IdTargetCollection`, falling back to the single `IdTarget` if `name` isn't found there (or is empty). Returns `null` if neither resolves. This is the id-only counterpart to `FetchTarget`, useful when you need the raw id rather than a resolved `Entity`.

**Parameters** \
`e` [Entity](../../Bang/Entities/Entity.html) \
`name` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

**Returns** \
[int?](https://learn.microsoft.com/en-us/dotnet/api/System.Nullable-1?view=net-7.0) \

#### FetchTarget(Entity, World, string)

```csharp
public static Entity? FetchTarget(this Entity e, World world, string name)
```

Resolves `FindTarget(e, name)` into an actual `Entity` by looking it up in `world`; returns `null` if no id is found or the entity no longer exists.

**Parameters** \
`e` [Entity](../../Bang/Entities/Entity.html) \
`world` [World](../../Bang/World.html) \
`name` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

**Returns** \
[Entity](../../Bang/Entities/Entity.html) \

#### AddDisableAgent(Entity)

```csharp
public static void AddDisableAgent(Entity e)
```

Increments a reference-counted `DisableAgentComponent` on `e` (creating it if absent). Because the count is additive, multiple independent systems can each disable the agent and it only becomes enabled again once every caller has matched their `AddDisableAgent` with a `RemoveDisableAgent`.

**Parameters** \
`e` [Entity](../../Bang/Entities/Entity.html) \

#### RemoveDisableAgent(Entity)

```csharp
public static void RemoveDisableAgent(Entity e)
```

Decrements `e`'s `DisableAgentComponent` reference count, removing the component entirely once it reaches zero. Pairs with `AddDisableAgent`; does nothing if the entity has no such component.

**Parameters** \
`e` [Entity](../../Bang/Entities/Entity.html) \

#### PauseAgent(Entity)

```csharp
public static void PauseAgent(Entity e)
```

Increments a reference-counted `AgentPauseRuntimeComponent` on `e` (creating it if absent), following the same additive pattern as `AddDisableAgent` so multiple systems can independently pause an agent's runtime behavior.

**Parameters** \
`e` [Entity](../../Bang/Entities/Entity.html) \

#### UnpauseAgent(Entity)

```csharp
public static void UnpauseAgent(Entity e)
```

Decrements `e`'s `AgentPauseRuntimeComponent` reference count, removing the component once it reaches zero. Pairs with `PauseAgent`.

**Parameters** \
`e` [Entity](../../Bang/Entities/Entity.html) \

#### PlayAnimationOverload(Entity, string, AnimationOverloadProperties, int, Guid?)

```csharp
public static void PlayAnimationOverload(this Entity e, string animation, AnimationOverloadProperties properties = AnimationOverloadProperties.Loop | AnimationOverloadProperties.IgnoreFacing, int offset = 0, Guid? customSprite = null)
```

Single-animation convenience overload of `PlayAnimationOverload(Entity, ImmutableArray<string>, AnimationOverloadProperties, int, Guid?)` — wraps `animation` in a one-element array and forwards to it.

**Parameters** \
`e` [Entity](../../Bang/Entities/Entity.html) \
`animation` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
`properties` [AnimationOverloadProperties](../../Murder/Services/AnimationOverloadProperties.html) \
`offset` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`customSprite` [Guid?](https://learn.microsoft.com/en-us/dotnet/api/System.Nullable-1?view=net-7.0) \

#### PlayAnimationOverload(Entity, ImmutableArray&lt;string&gt;, AnimationOverloadProperties, int, Guid?)

```csharp
public static void PlayAnimationOverload(this Entity e, ImmutableArray<string> animations, AnimationOverloadProperties properties = AnimationOverloadProperties.Loop | AnimationOverloadProperties.IgnoreFacing, int offset = 0, Guid? customSprite = null)
```

Sets an `AnimationOverloadComponent` on `e` that temporarily plays `animations` on top of (overriding) its normal sprite animation state, translating each `AnimationOverloadProperties` flag into the matching component field: `Disappear` appends a `"_"` terminator frame and forces `Loop` (so the overload ends by disappearing rather than looping visibly), `FlipHorizontal` sets `ImageFlip.Horizontal`, `LockTo4Directions` restricts `SupportedDirections` to 4, and `LockHorizontal`/`LockVertical` constrain `SupportedOrientation`. Clears any pending animation-complete flags so the overload starts cleanly. Use this for temporary animation overrides driven by abilities/reactions/cutscenes that should play independent of the entity's usual state-machine-driven animation.

**Parameters** \
`e` [Entity](../../Bang/Entities/Entity.html) \
`animations` [ImmutableArray\<string\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \
`properties` [AnimationOverloadProperties](../../Murder/Services/AnimationOverloadProperties.html) \
`offset` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`customSprite` [Guid?](https://learn.microsoft.com/en-us/dotnet/api/System.Nullable-1?view=net-7.0) \

#### AddVerticalVelocity(Entity, float)

```csharp
public static void AddVerticalVelocity(Entity entity, float zVelocity)
```

Adds `zVelocity` to the entity's existing `VerticalPositionComponent.ZVelocity`, or creates a new `VerticalPositionComponent` (at height `1`, marked active) with `zVelocity` as its initial velocity if the entity doesn't have one yet. Use this for jump impulses, knockback-with-height, or any gameplay effect that gives an entity upward/downward momentum along its vertical (Z) axis.

**Parameters** \
`entity` [Entity](../../Bang/Entities/Entity.html) \
`zVelocity` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### IsAnimatingStartingWith(Entity, string)

```csharp
public static bool IsAnimatingStartingWith(this Entity e, string animation)
```

Returns `true` if the entity's currently playing animation — checked on its `SpriteComponent.CurrentAnimation` first, then its `AnimationOverloadComponent.CurrentAnimation` — starts with `animation` (case-insensitive). Use this to test animation state by prefix, e.g. checking `"attack"` matches `"attack_left"`, without needing an exact clip name.

**Parameters** \
`e` [Entity](../../Bang/Entities/Entity.html) \
`animation` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

⚡
