# ActivateOnStartComponent

**Namespace:** Murder.Components.Utilities \
**Assembly:** Murder.dll

```csharp
public sealed struct ActivateOnStartComponent : IComponent
```

Activates (or, if configured, deactivates) this entity once, the first time `ActivateOnStartSystem` runs at world startup.

**Implements:** _[IComponent](../../../Bang/Components/IComponent.html)_

**Intent:** Lets an entity's initial active/inactive state be authored declaratively instead of requiring a bespoke one-off startup system. `ActivateOnStartSystem` filters for this component and, for every matching entity, optionally checks `OnlyWhen` and then calls `Entity.Activate()` (or `Entity.Deactivate()` if `DeactivateInstead` is set), before cleaning the component up according to `After`.

**Use-case:** Attach to an entity that should start deactivated in the prefab/level but come alive on level load (e.g. content gated behind a story flag), or the inverse — an entity that starts active but should be deactivated as soon as the world begins, unless a condition holds. Use `OnlyWhen` to gate the toggle on an [ICondition](../../../Murder/Core/Conditions/ICondition.html), and `After` to control what happens to the component/entity once the toggle has been applied (e.g. remove the component so it doesn't re-trigger on a later reload, or destroy the entity outright).

### ⭐ Constructors

```csharp
public ActivateOnStartComponent()
```

Default constructor. `After` defaults to `AfterInteractRule.Always`, `DeactivateInstead` to `false`, and `OnlyWhen` to `null` (no gating condition).

```csharp
public ActivateOnStartComponent(AfterInteractRule after, bool deactivateInstead)
```

Creates the component with an explicit cleanup rule and activation direction, and no condition gating it (the toggle always applies).

**Parameters** \
`after` [AfterInteractRule](../../../Murder/Components/AfterInteractRule.html) — what to do with the component/entity once the toggle has been applied. \
`deactivateInstead` [bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) — when `true`, deactivates the entity instead of activating it. \

### ⭐ Properties

#### After

```csharp
public readonly AfterInteractRule After;
```

What to do with this component (or the entity) once the activation/deactivation has been applied — e.g. remove the component so it doesn't re-trigger, or destroy the entity entirely.

**Returns** \
[AfterInteractRule](../../../Murder/Components/AfterInteractRule.html) \

#### DeactivateInstead

```csharp
public readonly bool DeactivateInstead;
```

When `true`, the entity is deactivated on start instead of activated.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### OnlyWhen

```csharp
public readonly ICondition OnlyWhen;
```

Optional condition that must be satisfied (evaluated against the current `World`) for the activation/deactivation to be applied. When `null`, the toggle always happens.

**Returns** \
[ICondition](../../../Murder/Core/Conditions/ICondition.html) \

⚡
