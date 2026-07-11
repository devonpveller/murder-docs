# InteractorComponent

**Namespace:** Murder.Interactions \
**Assembly:** Murder.dll

```csharp
public sealed struct InteractorComponent : IComponent
```

Component used to signal that an entity is able to interact with other objects.

**Intent:** Marks an entity as an active interactor in the ECS world.

**Use-case:** Attach to the player entity (or any NPC) so that the engine's interaction systems recognise it as a source that can trigger `IInteraction` responses on nearby entities.

**Implements:** _[IComponent](../../Bang/Components/IComponent.html)_



⚡