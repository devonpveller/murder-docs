# DestroyAfterSecondsComponent

**Namespace:** Murder.Components.Utilities \
**Assembly:** Murder.dll

```csharp
public sealed struct DestroyAfterSecondsComponent : IComponent
```

Schedules an entity to be destroyed after a fixed number of seconds.

**Intent:** Auto-expire a temporary entity after a set lifetime without external system logic.

**Use-case:** Attach to projectiles, particles, or temporary effect entities; set `Lifespan` to the number of seconds before automatic destruction.

**Implements:** _[IComponent](../../../Bang/Components/IComponent.html)_

### ⭐ Properties
#### Lifespan
```csharp
public float Lifespan { get; public set; }
```

Number of seconds after which the entity is automatically destroyed.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \


⚡