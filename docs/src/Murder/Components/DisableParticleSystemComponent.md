# DisableParticleSystemComponent

**Namespace:** Murder.Components \
**Assembly:** Murder.dll

```csharp
public sealed struct DisableParticleSystemComponent : IComponent
```

Marker component that stops a particle system entity from emitting new particles.

**Implements:** _[IComponent](../../Bang/Components/IComponent.html)_

**Intent:** Pauses particle emission without destroying the particle system entity or its [ParticleSystemComponent](../../Murder/Components/ParticleSystemComponent.html) configuration, so the emitter can be turned back on later with its original settings intact.

**Use-case:** Attach to an entity that also has a `ParticleSystemComponent` to halt its emission (e.g., an engine's exhaust particles when the engine turns off). `ParticleDisableTrackerSystem` watches for this component being added or removed: when added, it deactivates the entity in the `WorldParticleSystemTracker`; when removed, it re-activates (and, if not already tracked, starts tracking) the entity so emission resumes.

⚡
