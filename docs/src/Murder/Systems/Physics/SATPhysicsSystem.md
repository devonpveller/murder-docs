# SATPhysicsSystem

**Namespace:** Murder.Systems.Physics \
**Assembly:** Murder.dll

```csharp
public class SATPhysicsSystem : IFixedUpdateSystem, ISystem
```

Runs SAT (Separating Axis Theorem) collision detection and applies collision response to solid physics entities.

**Intent:** Detects and resolves solid-body collisions using the Separating Axis Theorem.

**Use-case:** Add to any world that requires solid physics resolution between entities with collision shapes.

**Implements:** _[IFixedUpdateSystem](../../../Bang/Systems/IFixedUpdateSystem.html), [ISystem](../../../Bang/Systems/ISystem.html)_

### ⭐ Constructors
```csharp
public SATPhysicsSystem()
```

### ⭐ Methods
#### FixedUpdate(Context)
```csharp
public virtual void FixedUpdate(Context context)
```

**Parameters** \
`context` [Context](../../../Bang/Contexts/Context.html) \



⚡