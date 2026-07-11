# DestroyAtTimeSystem

**Namespace:** Murder.Systems \
**Assembly:** Murder.dll

```csharp
public class DestroyAtTimeSystem : IUpdateSystem, ISystem
```

Checks entities with `DestroyAtTimeComponent` each update and destroys or deactivates them once `Game.Now` surpasses their scheduled time.

**Intent:** Implements timed entity lifecycle management by removing or deactivating entities at a pre-specified game time.

**Use-case:** Attach `DestroyAtTimeComponent` to any temporary entity (projectile, visual effect, timer) and this system will clean it up automatically when the time is reached.

**Implements:** _[IUpdateSystem](../../Bang/Systems/IUpdateSystem.html), [ISystem](../../Bang/Systems/ISystem.html)_

### ⭐ Constructors
```csharp
public DestroyAtTimeSystem()
```

### ⭐ Methods
#### DestroyEntity(World, Entity)
```csharp
protected virtual void DestroyEntity(World world, Entity e)
```

Called when the scheduled time is reached; override to customize destruction behaviour (default implementation destroys the entity).

**Parameters** \
`world` [World](../../Bang/World.html) \
`e` [Entity](../../Bang/Entities/Entity.html) \

#### Update(Context)
```csharp
public virtual void Update(Context context)
```

Iterates all entities with `DestroyAtTimeComponent` and destroys or deactivates each one whose scheduled time has passed.

**Parameters** \
`context` [Context](../../Bang/Contexts/Context.html) \



⚡