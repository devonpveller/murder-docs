# DestroyAfterSecondsComponent

**Namespace:** Murder.Components.Utilities \
**Assembly:** Murder.dll

```csharp
public sealed struct DestroyAfterSecondsComponent : IComponent
```

Schedules an entity to be destroyed a fixed number of seconds after it was created.

**Implements:** _[IComponent](../../../Bang/Components/IComponent.html)_

**Intent:** Works together with [CreatedAtComponent](../../../Murder/Components/CreatedAtComponent.html): `CreationTimeSystem` automatically stamps a newly-created entity with a `CreatedAtComponent` the moment this component is added, and `DestroyAfterSystem` then compares `CreatedAtComponent.When + Lifespan` against the current game time each fixed update, calling `Entity.Destroy()` once that time has passed.

**Use-case:** Attach to projectiles, particles, or other temporary effect entities; set `Lifespan` to the number of seconds before automatic destruction, and the entity cleans itself up without any other system having to track its lifetime.

### ⭐ Properties

#### Lifespan

```csharp
public float Lifespan { get; init; }
```

Number of seconds, counted from the entity's creation time, after which the entity is automatically destroyed.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

⚡
