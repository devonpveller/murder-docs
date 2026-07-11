# DisableEntityComponent

**Namespace:** Murder.Components.Effects \
**Assembly:** Murder.dll

```csharp
public sealed struct DisableEntityComponent : IComponent
```

Component that temporarily excludes this entity to exist within the world.

**Implements:** _[IComponent](../../../Bang/Components/IComponent.html)_

**Intent:** Hides and deactivates an entity without destroying it, so it can be re-enabled later.

**Use-case:** Attach to temporarily hide an entity (e.g., a chest that has been opened, or an NPC that should not appear yet); remove the component to restore the entity to the world.



⚡