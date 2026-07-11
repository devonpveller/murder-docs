# ParticleDestroyerSystem

**Namespace:** Murder.Systems.Graphics \
**Assembly:** Murder.dll

```csharp
public class ParticleDestroyerSystem : IFixedUpdateSystem, ISystem
```

Removes expired particle entities from the world each fixed update.

**Intent:** Cleans up particle entities whose lifetime has expired.

**Use-case:** Include in any world that uses Murder's particle system to prevent accumulation of dead particle entities.

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

**Parameters** \
`context` [Context](../../../Bang/Contexts/Context.html) \



⚡