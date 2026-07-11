# IMessagerSystem

**Namespace:** Bang.Systems \
**Assembly:** Bang.dll

```csharp
public abstract IMessagerSystem : ISystem
```

A reactive system that reacts to messages getting fired on an entity. Unlike
            [IReactiveSystem](../../Bang/Systems/IReactiveSystem.html) - which batches notifications about component changes and
            delivers them once at the end of the frame - [IMessagerSystem](../../Bang/Systems/IMessagerSystem.html) is invoked
            synchronously, one call per message, right when `Entity.SendMessage` fires it. A
            system must be decorated with [MessagerAttribute](../../Bang/Systems/MessagerAttribute.html) declaring which
            [IMessage](../../Bang/Components/IMessage.html) types it wants to hear about; [World](../../Bang/World.html) uses that
            attribute to build the internal message watcher that
            routes matching messages here. Combine with [FilterAttribute](../../Bang/Systems/FilterAttribute.html) to further
            restrict which entities' messages actually reach the system.

**Implements:** _[ISystem](../../Bang/Systems/ISystem.html)_

### ⭐ Methods
#### OnMessage(World, Entity, IMessage)
```csharp
public abstract void OnMessage(World world, Entity entity, IMessage message)
```

Called once a message is fired from `entity`, for each
            [IMessage](../../Bang/Components/IMessage.html) type declared in this system's [MessagerAttribute](../../Bang/Systems/MessagerAttribute.html).

**Parameters** \
`world` [World](../../Bang/World.html) \
`entity` [Entity](../../Bang/Entities/Entity.html) \
`message` [IMessage](../../Bang/Components/IMessage.html) \



⚡
