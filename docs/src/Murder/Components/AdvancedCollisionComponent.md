# AdvancedCollisionComponent

**Namespace:** Murder.Components \
**Assembly:** Murder.dll

```csharp
public sealed struct AdvancedCollisionComponent : IComponent
```

Marker component that opts an entity into the advanced (per-entity collision-mask) physics pipeline.

**Implements:** _[IComponent](../../Bang/Components/IComponent.html)_

**Intent:** Signals the physics system to use the entity's `CustomCollisionMask` instead of the world-default layer rules.

**Use-case:** Attach to any entity that needs non-standard collision filtering — for example a projectile that should only collide with enemies but not walls, or a trigger zone that ignores the player.



⚡