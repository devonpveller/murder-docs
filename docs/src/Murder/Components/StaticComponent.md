# StaticComponent

**Namespace:** Murder.Components \
**Assembly:** Murder.dll

```csharp
public sealed struct StaticComponent : IComponent
```

Marker component that flags an entity as non-moving, allowing physics and rendering systems to skip per-frame updates for it.

**Intent:** Signal that an entity will never change position so the engine can apply static-object optimisations.

**Use-case:** Attach to walls, floors, fixed props, or any entity whose position and shape will never change at runtime.

**Implements:** _[IComponent](../../Bang/Components/IComponent.html)_



⚡