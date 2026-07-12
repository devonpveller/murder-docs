# RandomizeAsepriteSystem

**Namespace:** Murder.Systems.Graphics \
**Assembly:** Murder.dll

```csharp
public class RandomizeAsepriteSystem : IReactiveSystem, ISystem
```

Reacts to [RandomizeSpriteComponent](../../../Murder/Components/RandomizeSpriteComponent.html) being added, or to the entity being reactivated, on an entity that also has a [SpriteComponent](../../../Murder/Components/SpriteComponent.html). It rolls whichever random variations the component requests — a random non-empty animation, a randomized animation start offset, a random cardinal facing with rotate-to-face enabled, and/or a horizontal flip — so entities that share the same sprite asset don't all look and animate in perfect lockstep.

**Intent:** Adds cosmetic variety to bulk-spawned entities that reuse the same sprite asset.

**Use-case:** Attach `RandomizeSpriteComponent` to entities spawned in bulk (foliage, decorations, tile clutter) so identical prefab instances don't all display the same animation frame, facing, or orientation.

**Implements:** _[IReactiveSystem](../../../Bang/Systems/IReactiveSystem.html), [ISystem](../../../Bang/Systems/ISystem.html)_

### ⭐ Constructors

```csharp
public RandomizeAsepriteSystem()
```

### ⭐ Methods

#### OnActivated(World, ImmutableArray<T>)

```csharp
public virtual void OnActivated(World world, ImmutableArray<T> entities)
```

Re-rolls the random variations for entities that were reactivated, delegating to the same logic as `OnAdded` so a pooled/reused entity looks freshly randomized again.

**Parameters** \
`world` [World](../../../Bang/World.html) \
`entities` [ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \

#### OnAdded(World, ImmutableArray<T>)

```csharp
public virtual void OnAdded(World world, ImmutableArray<T> entities)
```

Applies the random variations requested by each entity's `RandomizeSpriteComponent`: optionally picks a random non-empty animation from the sprite's asset, randomizes the animation start time, assigns a random cardinal facing with rotation-to-face enabled, and/or flips the sprite horizontally with a 50% chance.

**Parameters** \
`world` [World](../../../Bang/World.html) \
`entities` [ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \

#### OnModified(World, ImmutableArray<T>)

```csharp
public virtual void OnModified(World world, ImmutableArray<T> entities)
```

Unused: this system only needs to react when `RandomizeSpriteComponent` is added or the entity is reactivated, so modifications are intentionally ignored.

**Parameters** \
`world` [World](../../../Bang/World.html) \
`entities` [ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \

#### OnRemoved(World, ImmutableArray<T>)

```csharp
public virtual void OnRemoved(World world, ImmutableArray<T> entities)
```

Unused: there is no cleanup to perform when `RandomizeSpriteComponent` is removed.

**Parameters** \
`world` [World](../../../Bang/World.html) \
`entities` [ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \

⚡
