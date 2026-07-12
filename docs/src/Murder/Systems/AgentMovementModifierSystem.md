# AgentMovementModifierSystem

**Namespace:** Murder.Systems \
**Assembly:** Murder.dll

```csharp
public class AgentMovementModifierSystem : IMessagerSystem, ISystem
```

Listens for `OnCollisionMessage` events on entities with `MovementModAreaComponent` and applies or removes movement-speed modifiers to agents as they enter or exit the area.

**Intent:** Applies area-based movement modifiers to agents when they enter or exit a designated movement-modification zone.

**Use-case:** Add to any world where you want environmental areas (e.g., mud, water, wind corridors) to dynamically alter agent movement speed.

**Implements:** _[IMessagerSystem](../../Bang/Systems/IMessagerSystem.html), [ISystem](../../Bang/Systems/ISystem.html)_

### ⭐ Constructors

```csharp
public AgentMovementModifierSystem()
```

### ⭐ Methods

#### OnMessage(World, Entity, IMessage)

```csharp
public virtual void OnMessage(World world, Entity entity, IMessage message)
```

Routes the collision message to `OnEnter` or `OnExit` depending on the collision direction, updating the `InsideMovementModAreaComponent` on the colliding entity.

**Parameters** \
`world` [World](../../Bang/World.html) \
`entity` [Entity](../../Bang/Entities/Entity.html) \
`message` [IMessage](../../Bang/Components/IMessage.html) \

⚡
