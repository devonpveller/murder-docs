# VerticalPhysicsSystem

**Namespace:** Murder.Systems.Physics \
**Assembly:** Murder.dll

```csharp
public class VerticalPhysicsSystem : IFixedUpdateSystem, ISystem
```

Handles vertical (Z-axis) physics for entities in top-down games that simulate height, including gravity and landing.

**Intent:** Simulates Z-axis gravity and height for entities in top-down perspective.

**Use-case:** Use in top-down games where entities can jump or fall, and vertical position affects rendering and collision layers.

**Implements:** _[IFixedUpdateSystem](../../../Bang/Systems/IFixedUpdateSystem.html), [ISystem](../../../Bang/Systems/ISystem.html)_

### ⭐ Constructors
```csharp
public VerticalPhysicsSystem()
```

### ⭐ Methods
#### FixedUpdate(Context)
```csharp
public virtual void FixedUpdate(Context context)
```

**Parameters** \
`context` [Context](../../../Bang/Contexts/Context.html) \



⚡