# ParticleSystemWorldTrackerComponent

**Namespace:** Murder.Components \
**Assembly:** Murder.dll

```csharp
public sealed struct ParticleSystemWorldTrackerComponent : IComponent
```

This tracks all the particle systems that are currently active in the world.

**Intent:** Maintain a world-level registry of all active particle system instances so they can be updated and rendered centrally each frame.

**Use-case:** Added once to the world entity by the particle system; access `Tracker` to query or manipulate the set of live particle emitters without iterating over individual entities.

**Implements:** _[IComponent](../../Bang/Components/IComponent.html)_

### ⭐ Constructors
```csharp
public ParticleSystemWorldTrackerComponent()
```

### ⭐ Properties
#### Tracker
```csharp
public readonly WorldParticleSystemTracker Tracker;
```

The shared tracker object that holds references to all currently active particle system instances in the world.

**Returns** \
[WorldParticleSystemTracker](../../Murder/Core/Particles/WorldParticleSystemTracker.html) \


⚡