# IgnoreUntilSystem

**Namespace:** Murder.Systems \
**Assembly:** Murder.dll

```csharp
public class IgnoreUntilSystem : IUpdateSystem, ISystem
```

Removes `IgnoreUntilComponent` from entities once `Game.Now` reaches or surpasses the stored timestamp, re-enabling them for interaction or processing.

**Intent:** Provides a time-based ignore gate that suppresses entity interactions until a specified moment in game time.

**Use-case:** Add `IgnoreUntilComponent` to an entity to temporarily prevent it from being processed (e.g., prevent re-triggering immediately after activation); this system lifts the suppression automatically.

**Implements:** _[IUpdateSystem](../../Bang/Systems/IUpdateSystem.html), [ISystem](../../Bang/Systems/ISystem.html)_

### ⭐ Constructors
```csharp
public IgnoreUntilSystem()
```

### ⭐ Methods
#### Update(Context)
```csharp
public virtual void Update(Context context)
```

Checks each entity's `IgnoreUntilComponent` timestamp; removes the component once `Game.Now` has reached or passed the scheduled time.

**Parameters** \
`context` [Context](../../Bang/Contexts/Context.html) \



⚡