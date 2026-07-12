# DoNotPersistEntityOnSaveComponent

**Namespace:** Murder.Components \
**Assembly:** Murder.dll

```csharp
public sealed struct DoNotPersistEntityOnSaveComponent : IComponent
```

Marker component that excludes an entity from being serialized when the game world is saved.

**Implements:** _[IComponent](../../Bang/Components/IComponent.html)_

**Intent:** Prevents transient runtime entities (effects, particles, temporary helpers) from being written into save files where they would be meaningless on reload. It works by carrying the `[DoNotPersistEntityOnSave]` attribute on itself; `SavedWorldBuilder.FilterComponents` checks every component type on an entity for that attribute and, if found on any of them, skips serializing the whole entity.

**Use-case:** Attach to any entity created at runtime that should not survive a save/load cycle. `EffectsServices.CreateQuickSprite` and `MonoWorld`'s internal setup both add it automatically to entities they spawn (quick visual-effect sprites, engine-internal helper entities); several other components (`QuadtreeComponent`, `HAAStarPathfindComponent`, `ParticleSystemTrackerComponent`, the `Story` watcher components, etc.) achieve the same exclusion by carrying the `[DoNotPersistEntityOnSave]` attribute directly instead of requiring this component to be added.

⚡
