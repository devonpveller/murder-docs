# InteractOnCollisionSystem

**Namespace:** Murder.Systems \
**Assembly:** Murder.dll

```csharp
public class InteractOnCollisionSystem : IMessagerSystem, ISystem
```

Interactors tag hightlights and interacts with InteractorComponents

**Intent:** Triggers interaction logic when a colliding entity (typically an agent, e.g. the player) enters or exits the bounds of an entity carrying `InteractOnCollisionComponent`. It centralizes the once-per-load/once-ever gating, custom enter/exit interaction lists, and optional deactivation-after-interaction behavior that would otherwise be duplicated across every collision-triggered interactable in the game.

**Use-case:** Attach `InteractOnCollisionComponent` to doors, pickups, or trigger zones; this system listens for `OnCollisionMessage` and, when the colliding entity is (or is the child of) an agent and isn't currently ignored via `IgnoreUntilComponent`, runs the configured `CustomEnterMessages`/`CustomExitMessages` interactions and sends the standard interact message on enter. Override `IsInteractAllowed` in a derived system to add game-specific gating (e.g. require a key item) without reimplementing the whole collision/once-per-load bookkeeping.

**Implements:** _[IMessagerSystem](../../Bang/Systems/IMessagerSystem.html), [ISystem](../../Bang/Systems/ISystem.html)_

### ⭐ Constructors

```csharp
public InteractOnCollisionSystem()
```

### ⭐ Methods

#### OnMessage(World, Entity, IMessage)

```csharp
public virtual void OnMessage(World world, Entity entity, IMessage message)
```

Handles an `OnCollisionMessage` for an entity with `InteractOnCollisionComponent`. Resolves the colliding entity as the interactor (requiring it, or its parent, to have an `AgentComponent`, and to not be destroyed or currently ignored), checks the `Once`/`OnceEveryLoad` flags and `IsInteractAllowed`, then on `CollisionDirection.Enter` runs `CustomEnterMessages` and sends the standard interact message, or on `CollisionDirection.Exit` runs `CustomExitMessages` (unless `SkipExitIfInteractorInside` is set and another hitbox/actor is still overlapping, via `IsInteractorInside`). If the interaction is single-use, it marks the entity as interacted, deactivates it, or removes `InteractOnCollisionComponent` depending on the configured flags.

**Parameters** \
`world` [World](../../Bang/World.html) \
`entity` [Entity](../../Bang/Entities/Entity.html) \
`message` [IMessage](../../Bang/Components/IMessage.html) \

#### IsInteractorInside(World, Entity, int)

```csharp
public static bool IsInteractorInside(World world, Entity e, int except)
```

Checks the entity's `CollisionCacheComponent` to see whether it is still overlapping any other entity (other than `except`) whose collider has the `HITBOX` or `ACTOR` layer. Used by `OnMessage` to decide whether an exit interaction should be suppressed because another valid interactor is still inside the trigger.

**Parameters** \
`world` [World](../../Bang/World.html) \
`e` [Entity](../../Bang/Entities/Entity.html) \
`except` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### IsInteractAllowed(World, Entity, Entity, InteractOnCollisionComponent, OnCollisionMessage)

```csharp
protected virtual bool IsInteractAllowed(World world, Entity interactor, Entity interacted, InteractOnCollisionComponent component, OnCollisionMessage message)
```

Extension point that gates whether a collision interaction is allowed to proceed; returns `true` by default. Override this in a derived system to add game-specific conditions (inventory checks, dialogue state, quest flags, etc.) without touching the surrounding once-per-load/enter/exit bookkeeping in `OnMessage`.

**Parameters** \
`world` [World](../../Bang/World.html) \
`interactor` [Entity](../../Bang/Entities/Entity.html) \
`interacted` [Entity](../../Bang/Entities/Entity.html) \
`component` [InteractOnCollisionComponent](../../Murder/Components/InteractOnCollisionComponent.html) \
`message` [OnCollisionMessage](../../Murder/Messages/Physics/OnCollisionMessage.html) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

⚡
