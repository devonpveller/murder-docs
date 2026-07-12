# AlwaysInCameraComponent

**Namespace:** Murder.Components.Graphics \
**Assembly:** Murder.dll

```csharp
public sealed struct AlwaysInCameraComponent : IComponent
```

Marker checked by the particle system tracker to skip camera-area culling for this entity's particle pool, so its particles keep simulating and emitting even while the entity itself is off-screen.

**Intent:** Particle systems are normally paused/culled when their owning entity leaves the camera's visible area, which is usually the right call for performance but wrong for effects that must keep running in the background (e.g. an off-screen fire or smoke source that should already be lit when the camera pans to it). `WorldParticleSystemTracker.Step` checks `entity.HasAlwaysInCamera()` and, when true, passes a `null` camera area to that entity's particle pool tracker instead of the real camera rectangle, disabling the culling check entirely for it.

**Use-case:** Add to an entity with a particle system component when its particles must always keep emitting/simulating regardless of camera position. As the source comment notes, this currently "only works for PARTICLES" — it has no effect on sprite rendering or other visibility systems.

**Implements:** _[IComponent](../../../Bang/Components/IComponent.html)_

⚡
