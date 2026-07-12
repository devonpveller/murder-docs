# ParticleDestroyerSystem

**Namespace:** Murder.Systems.Graphics \
**Assembly:** Murder.dll

```csharp
public class ParticleDestroyerSystem : IFixedUpdateSystem, ISystem
```

Destroys entities carrying a [ParticleSystemComponent](../../../Murder/Components/ParticleSystemComponent.html) once their emitter has both stopped emitting and finished playing out its already-spawned particles. Whether an emitter still has live particles is determined by asking the world's `WorldParticleSystemTracker` (fetched via the unique `ParticleSystemWorldTrackerComponent`) whether it still tracks any particles for that entity. Only entities whose component has `DestroyWhenEmpty` set to `true` are eligible for removal, so looping/ambient particle systems that should persist indefinitely are left untouched.

**Intent:** Cleans up one-shot particle-emitter entities (explosions, impact effects, etc.) after they finish, instead of requiring the game code to track and destroy them manually.

**Use-case:** Include in any world that uses Murder's particle system alongside `ParticleSystemComponent(asset, destroy: true)` so spent one-shot effects don't accumulate as dead entities. If the world has no particle tracker set up yet (no `ParticleSystemWorldTrackerComponent`), this system is a no-op.

**Implements:** _[IFixedUpdateSystem](../../../Bang/Systems/IFixedUpdateSystem.html), [ISystem](../../../Bang/Systems/ISystem.html)_

### ⭐ Constructors

```csharp
public ParticleDestroyerSystem()
```

### ⭐ Methods

#### FixedUpdate(Context)

```csharp
public virtual void FixedUpdate(Context context)
```

For every entity with a `ParticleSystemComponent` flagged `DestroyWhenEmpty`, destroys it once the world's particle tracker reports it no longer has any live particles.

**Parameters** \
`context` [Context](../../../Bang/Contexts/Context.html) \

⚡
