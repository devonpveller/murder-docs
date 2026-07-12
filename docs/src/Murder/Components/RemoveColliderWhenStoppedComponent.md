# RemoveColliderWhenStoppedComponent

**Namespace:** Murder.Components \
**Assembly:** Murder.dll

```csharp
public sealed struct RemoveColliderWhenStoppedComponent : IComponent
```

Marker component that instructs `RemoveColliderWhenStoppedSystem` to strip the entity's collider the moment its velocity component is removed.

**Intent:** Automatically clean up a collider once a moving entity comes to rest, instead of leaving it as a permanent obstacle.

**Use-case:** Attach to projectiles, thrown items, or sliding debris. `SATPhysicsSystem` removes an entity's [VelocityComponent](../../Murder/Components/VelocityComponent.html) once its velocity decays below a minimum threshold (i.e. it has effectively stopped moving); `RemoveColliderWhenStoppedSystem` watches for that removal on entities that also carry this component and a [ColliderComponent](../../Murder/Components/ColliderComponent.html), and removes the collider so the settled entity stops participating in collision checks.

**Implements:** _[IComponent](../../Bang/Components/IComponent.html)_

⚡
