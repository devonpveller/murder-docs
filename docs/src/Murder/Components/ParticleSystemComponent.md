# ParticleSystemComponent

**Namespace:** Murder.Components \
**Assembly:** Murder.dll

```csharp
public sealed struct ParticleSystemComponent : IComponent
```

References a `ParticleSystemAsset` to be instantiated and emitted at this entity's position.

**Intent:** Attach a particle emitter to an entity so the particle system renders the configured effect at runtime.

**Use-case:** Add with the GUID of the desired particle effect asset; set `DestroyWhenEmpty` to `true` for one-shot effects (e.g. explosions) so the entity is cleaned up automatically after all particles fade.

**Implements:** _[IComponent](../../Bang/Components/IComponent.html)_

### ⭐ Constructors

```csharp
public ParticleSystemComponent(Guid asset, bool destroy)
```

**Parameters** \
`asset` [Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \
`destroy` [bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

### ⭐ Properties

#### Asset

```csharp
public readonly Guid Asset;
```

GUID of the `ParticleSystemAsset` that defines the emitter behavior and particle parameters.

**Returns** \
[Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \

#### DestroyWhenEmpty

```csharp
public readonly bool DestroyWhenEmpty;
```

When `true`, the entity is destroyed automatically once all emitted particles have expired and no new ones are being spawned.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

⚡
