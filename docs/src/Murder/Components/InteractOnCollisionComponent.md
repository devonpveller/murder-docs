# InteractOnCollisionComponent

**Namespace:** Murder.Components \
**Assembly:** Murder.dll

```csharp
public sealed struct InteractOnCollisionComponent : IComponent
```

Triggers the entity's interactive components when another entity (typically the player agent) enters, stays within, or exits its collision bounds.

**Intent:** Enable proximity-based interactions, such as opening a door, starting a dialogue, or activating a trap, driven by physical collision overlap, with fine-grained control over who can trigger it and how many times via the `InteractOnCollisionFlags` bit flags.

**Use-case:** Add to a trigger zone entity; set `Flags` with `InteractOnCollisionFlags.PlayerOnly` to restrict activation to the player, `InteractOnCollisionFlags.Once`/`OnceEveryLoad` to fire only the first time, and populate `CustomEnterMessages`/`CustomExitMessages` to trigger interactions beyond the ones already on this entity. Consumed by `InteractOnCollisionSystem`, which listens for collision messages and reacts according to `Flags`.

**Implements:** _[IComponent](../../Bang/Components/IComponent.html)_

### ⭐ Constructors

```csharp
public InteractOnCollisionComponent()
```

Creates a component with no flags set: any actor can trigger it, repeatedly, with no exit suppression.

```csharp
public InteractOnCollisionComponent(InteractOnCollisionFlags flags)
```

Creates a component configured with the given `flags`.

**Parameters** \
`flags` `InteractOnCollisionFlags` \

### ⭐ Properties

#### CustomEnterMessages

```csharp
public readonly ImmutableArray<IInteractiveComponent> CustomEnterMessages;
```

Additional interactions triggered when a valid actor enters the collision area, on top of any [IInteractiveComponent](../../Bang/Interactions/IInteractiveComponent.html) already present on this entity.

**Returns** \
[ImmutableArray\<IInteractiveComponent\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \

#### CustomExitMessages

```csharp
public readonly ImmutableArray<IInteractiveComponent> CustomExitMessages;
```

Additional interactions triggered when a valid actor exits the collision area. Only fires when the exiting actor was previously inside and this list is non-empty (see `InteractOnCollisionFlags.SkipExitIfInteractorInside` for suppressing this while another valid actor remains inside).

**Returns** \
[ImmutableArray\<IInteractiveComponent\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \

#### Flags

```csharp
public readonly InteractOnCollisionFlags Flags { get; init; }
```

Combination of `InteractOnCollisionFlags` controlling who can trigger this interaction, whether it can fire more than once, and how exit notifications behave. Available flags are `None`, `PlayerOnly` (only the player entity can activate it), `Once` (deactivates after the first successful interaction for the lifetime of the entity), `OnceEveryLoad` (like `Once`, but the "already interacted" state persists across map reloads), and `SkipExitIfInteractorInside` (skip the exit notification if another valid actor is still inside the area).

**Returns** \
`InteractOnCollisionFlags` \

⚡
