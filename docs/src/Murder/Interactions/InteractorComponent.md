# InteractorComponent

**Namespace:** Murder.Interactions \
**Assembly:** Murder.dll

```csharp
public sealed struct InteractorComponent : IComponent
```

Empty marker component used to tag an entity as an interactor — an entity that can initiate interactions with other entities, as opposed to being the target/recipient of one.

**Intent:** Marks an entity as an active interactor in the ECS world.

**Use-case:** Attach to the player entity (or any NPC) so systems and filters (`[Filter(typeof(InteractorComponent))]`) can distinguish interactor entities from entities that are merely interactive but never initiate interactions themselves. It carries no data.

**Implements:** _[IComponent](../../Bang/Components/IComponent.html)_

⚡
