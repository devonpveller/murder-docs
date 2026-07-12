# AnimationEventBroadcastSystem

**Namespace:** Murder.Systems \
**Assembly:** Murder.dll

```csharp
public class AnimationEventBroadcastSystem : IMessagerSystem, ISystem
```

Listens for `AnimationEventMessage` on entities with `AnimationEventBroadcasterComponent` and forwards the event to all registered listener entities.

**Intent:** Relays animation events from a source entity to a set of registered listeners so remote objects can react to animation milestones.

**Use-case:** Use when an animation on one entity should trigger logic (e.g., sound or particle burst) on other entities by listing them in an `AnimationEventBroadcasterComponent`.

**Implements:** _[IMessagerSystem](../../Bang/Systems/IMessagerSystem.html), [ISystem](../../Bang/Systems/ISystem.html)_

### ⭐ Constructors

```csharp
public AnimationEventBroadcastSystem()
```

### ⭐ Methods

#### OnMessage(World, Entity, IMessage)

```csharp
public virtual void OnMessage(World world, Entity entity, IMessage message)
```

Forwards the received `AnimationEventMessage` to every active entity listed in the broadcaster's target set; removes unreachable entities from the broadcast list.

**Parameters** \
`world` [World](../../Bang/World.html) \
`entity` [Entity](../../Bang/Entities/Entity.html) \
`message` [IMessage](../../Bang/Components/IMessage.html) \

⚡
