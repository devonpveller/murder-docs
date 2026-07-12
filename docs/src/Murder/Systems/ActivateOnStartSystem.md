# ActivateOnStartSystem

**Namespace:** Murder.Systems \
**Assembly:** Murder.dll

```csharp
public class ActivateOnStartSystem : IStartupSystem, ISystem
```

Runs once at world startup and activates (or deactivates) every entity carrying an `ActivateOnStartComponent`, optionally gated by a condition, then applies the component's configured post-trigger cleanup rule.

**Intent:** Lets level/entity data declare "this entity should turn on (or off) as soon as the world starts" without needing a bespoke startup system for each case. It is the startup-time counterpart to rule/interaction-driven activation systems: instead of reacting to a blackboard rule or a collision, it fires unconditionally on `Start`, optionally filtered by an `ICondition`.

**Use-case:** Attach `ActivateOnStartComponent` to any entity that should be activated or deactivated the moment the world loads — for example, enabling a trigger volume only after a prerequisite condition is met, or disabling decorative entities that should start hidden. Set `DeactivateInstead` to flip the effect from activate to deactivate, and use `After` (an `AfterInteractRule`) to control whether the component is removed, the whole entity is destroyed, or nothing further happens once the activation has been applied.

**Implements:** _[IStartupSystem](../../Bang/Systems/IStartupSystem.html), [ISystem](../../Bang/Systems/ISystem.html)_

### ⭐ Constructors

```csharp
public ActivateOnStartSystem()
```

### ⭐ Methods

#### Start(Context)

```csharp
public virtual void Start(Context context)
```

For every matching entity, evaluates `ActivateOnStartComponent.OnlyWhen` (if set) and skips the entity if the condition isn't satisfied; otherwise activates or deactivates the entity depending on `DeactivateInstead`, then applies the component's `AfterInteractRule` (`InteractOnlyOnce`/`RemoveComponent` removes `ActivateOnStartComponent`, `Destroy` destroys the entity, and any other value leaves the entity as-is).

**Parameters** \
`context` [Context](../../Bang/Contexts/Context.html) \

⚡
