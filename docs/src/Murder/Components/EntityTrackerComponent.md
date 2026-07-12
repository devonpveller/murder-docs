# EntityTrackerComponent

**Namespace:** Murder.Components \
**Assembly:** Murder.dll

```csharp
public sealed struct EntityTrackerComponent : IComponent
```

This is a component used to track other entities within the world.

**Implements:** _[IComponent](../../Bang/Components/IComponent.html)_

**Intent:** Stores a lightweight, serializable reference (by entity ID) from one entity to another, so a system can resolve `Target` via `world.TryGetEntity(Target)` without needing a direct object reference. It is marked `[RuntimeOnly]` (never authored as a prefab field) and `[PersistOnSave]` (unlike most runtime-only components, an instance survives a save/load cycle intact), which fits its purpose as a runtime link that needs to keep pointing at the same entity across saves.

**Use-case:** There is no built-in Murder system that reads this component today — it exists as a general-purpose "entity A points at entity B" building block for game-specific systems (e.g. a follower, a targeting reticle, or a linked pair of entities) to attach to a tracking entity and set `Target` to the ID of the entity being tracked, then resolve it each frame with `world.TryGetEntity(Target)`.

### ⭐ Constructors

```csharp
public EntityTrackerComponent(int target)
```

**Parameters** \
`target` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

### ⭐ Properties

#### Target

```csharp
public readonly int Target;
```

Id of the target entity.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

⚡
