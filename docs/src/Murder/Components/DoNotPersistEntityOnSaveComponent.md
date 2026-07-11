# DoNotPersistEntityOnSaveComponent

**Namespace:** Murder.Components \
**Assembly:** Murder.dll

```csharp
public sealed struct DoNotPersistEntityOnSaveComponent : IComponent
```

Marker component that excludes an entity from being serialized when the game world is saved.

**Implements:** _[IComponent](../../Bang/Components/IComponent.html)_

**Intent:** Prevents transient runtime entities (effects, particles, temporary helpers) from being written into save files where they would be meaningless on reload.

**Use-case:** Attach to any entity created at runtime that should not survive a save/load cycle, such as visual effects, runtime-spawned enemies, or temporary UI entities.



⚡