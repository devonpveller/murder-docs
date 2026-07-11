# RemoveColliderWhenStoppedComponent

**Namespace:** Murder.Components \
**Assembly:** Murder.dll

```csharp
public sealed struct RemoveColliderWhenStoppedComponent : IComponent
```

Marker component that instructs the engine to remove the entity's collider once its velocity reaches zero.

**Intent:** Automatically clean up a collider when a moving entity (e.g. a projectile) stops.

**Use-case:** Attach to projectiles or sliding objects so their collider is removed the moment they come to rest, preventing ghost collisions.

**Implements:** _[IComponent](../../Bang/Components/IComponent.html)_



⚡