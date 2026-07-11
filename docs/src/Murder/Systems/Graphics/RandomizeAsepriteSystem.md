# RandomizeAsepriteSystem

**Namespace:** Murder.Systems.Graphics \
**Assembly:** Murder.dll

```csharp
public class RandomizeAsepriteSystem : IReactiveSystem, ISystem
```

Reacts to `RandomizeSpriteComponent` being added and picks a random animation frame or sprite variant.

**Intent:** Assigns a random animation variant to new entities with `RandomizeSpriteComponent`.

**Use-case:** Use to add visual variety to entities (e.g., foliage, decorations) that share a sprite but should start on a random frame.

**Implements:** _[IReactiveSystem](../../../Bang/Systems/IReactiveSystem.html), [ISystem](../../../Bang/Systems/ISystem.html)_

### ⭐ Constructors
```csharp
public RandomizeAsepriteSystem()
```

### ⭐ Methods
#### OnAdded(World, ImmutableArray<T>)
```csharp
public virtual void OnAdded(World world, ImmutableArray<T> entities)
```

**Parameters** \
`world` [World](../../../Bang/World.html) \
`entities` [ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \

#### OnModified(World, ImmutableArray<T>)
```csharp
public virtual void OnModified(World world, ImmutableArray<T> entities)
```

**Parameters** \
`world` [World](../../../Bang/World.html) \
`entities` [ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \

#### OnRemoved(World, ImmutableArray<T>)
```csharp
public virtual void OnRemoved(World world, ImmutableArray<T> entities)
```

**Parameters** \
`world` [World](../../../Bang/World.html) \
`entities` [ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \



⚡