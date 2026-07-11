# FreeMovementComponent

**Namespace:** Murder.Components \
**Assembly:** Murder.dll

```csharp
public sealed struct FreeMovementComponent : IComponent
```

Marks an entity to receive free, unconstrained movement input in any direction, bypassing agent pathfinding and gravity.

**Intent:** Enable direct positional movement for entities that should respond to raw input without physics-based constraints.

**Use-case:** Add to the player entity when switching into a free-roam or debug mode; set `Flags` to control whether tiles are respected or whether the component persists across saves.

**Implements:** _[IComponent](../../Bang/Components/IComponent.html)_



⚡