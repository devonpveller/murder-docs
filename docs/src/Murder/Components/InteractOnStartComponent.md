# InteractOnStartComponent

**Namespace:** Murder.Components \
**Assembly:** Murder.dll

```csharp
public sealed struct InteractOnStartComponent : IComponent
```

Triggers the entity's interactive components exactly once, on world startup, without requiring any player input or collision.

**Intent:** Run an interaction at world-load time, such as applying initial state changes or starting a cutscene, without requiring any player input or external trigger. Optionally gate the interaction on a list of `ICondition`s and control whether the entity is destroyed after firing.

**Use-case:** Add to entities that should execute an interaction immediately on spawn (e.g. a level intro sequence, an auto-opening door, or a one-time spawn effect). Handled by `InteractOnStartSystem`, which runs during startup for every entity carrying this component, checks `Conditions` (if any), sends the interact message, and then destroys the entity if `Flags` includes `InteractOnStartFlags.OnlyOnce`.

**Implements:** _[IComponent](../../Bang/Components/IComponent.html)_

### ⭐ Constructors

```csharp
public InteractOnStartComponent()
```

Creates a component with no conditions (always fires) and default flags (entity is kept after firing).

```csharp
public InteractOnStartComponent(ImmutableArray<ICondition> conditions, InteractOnStartFlags flags)
```

Creates a component that only fires if `conditions` are satisfied, with the given post-fire `flags`.

**Parameters** \
`conditions` `ImmutableArray<ICondition>` \
`flags` `InteractOnStartFlags` \

### ⭐ Properties

#### Conditions

```csharp
public readonly ImmutableArray<ICondition>? Conditions;
```

Optional gate on the interaction: when set, the interaction only fires if every condition in this list is satisfied; when `null`, the interaction always fires unconditionally.

**Returns** \
[ImmutableArray\<ICondition\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0)? \

#### Flags

```csharp
public readonly InteractOnStartFlags Flags;
```

Controls what happens to the entity after the interaction fires. `None` (the default) fires once at startup and leaves the entity and component in place; `OnlyOnce` destroys the entity after firing, guaranteeing the interaction can never run again for it.

**Returns** \
`InteractOnStartFlags` \

⚡
