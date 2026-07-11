# DisableParticleSystemComponent

**Namespace:** Murder.Components \
**Assembly:** Murder.dll

```csharp
public sealed struct DisableParticleSystemComponent : IComponent
```

Marker component that stops a particle system entity from emitting new particles.

**Implements:** _[IComponent](../../Bang/Components/IComponent.html)_

**Intent:** Pauses particle emission without destroying the particle system entity or its configuration.

**Use-case:** Attach to a particle emitter entity to halt emission (e.g., when an engine turns off); remove it to resume emission.



⚡