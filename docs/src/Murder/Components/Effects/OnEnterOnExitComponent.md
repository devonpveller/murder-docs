# OnEnterOnExitComponent

**Namespace:** Murder.Components.Effects \
**Assembly:** Murder.dll

```csharp
public sealed struct OnEnterOnExitComponent : IComponent
```

Declares an area-trigger behavior for an entity with a collider: pairs an optional enter interaction and exit interaction with the collision events fired when a qualifying entity enters or leaves this entity's collider.

**Implements:** _[IComponent](../../../Bang/Components/IComponent.html)_

**Intent:** Acts as authoring data for trigger volumes such as "play a sound while inside this area and stop it on exit" or "run an interaction when the player walks through this zone". The level/sound editor's area-creation helpers build entities carrying this component paired with a `BoxShape` collider on the `TRIGGER` collision layer. [Kind](#kind) and [TriggerOnLayer](#triggeronlayer) control which entities are allowed to trigger the area, and [Target](#target) controls which entity the configured interactions are applied to when they fire.

**Use-case:** Attach to a trigger-zone entity (typically created through the level editor's "trigger when entering or exiting area" tooling) and configure [OnEnter](#onenter)/[OnExit](#onexit) with the desired [IInteractiveComponent](../../../Bang/Interactions/IInteractiveComponent.html) actions — for example, a `SetSoundParameterOnInteraction` pair to toggle an ambience parameter, or a `PlayEventInteraction`/`StopEventInteraction` pair to start and stop a sound while inside the area.

### ⭐ Constructors

```csharp
public OnEnterOnExitComponent()
```

Default constructor. `OnEnter` and `OnExit` are left `null` and `Kind` defaults to `Player`.

```csharp
public OnEnterOnExitComponent(IInteractiveComponent onEnter, IInteractiveComponent onExit)
```

Creates the component with both the enter and exit interactions set, using the default `Kind` (player-only).

**Parameters** \
`onEnter` [IInteractiveComponent](../../../Bang/Interactions/IInteractiveComponent.html) — interaction to run when a qualifying entity enters the area. \
`onExit` [IInteractiveComponent](../../../Bang/Interactions/IInteractiveComponent.html) — interaction to run when a qualifying entity leaves the area. \

### ⭐ Properties

#### OnEnter

```csharp
public readonly IInteractiveComponent OnEnter;
```

The interaction to run when a qualifying entity enters this entity's collision area. `null` if no enter behavior is configured.

**Returns** \
[IInteractiveComponent](../../../Bang/Interactions/IInteractiveComponent.html) \

#### OnExit

```csharp
public readonly IInteractiveComponent OnExit;
```

The interaction to run when a qualifying entity leaves this entity's collision area. `null` if no exit behavior is configured.

**Returns** \
[IInteractiveComponent](../../../Bang/Interactions/IInteractiveComponent.html) \

#### Target

```csharp
public readonly TargetEntity Target;
```

Which entity (the interactor that triggered the area, or another target) the [OnEnter](#onenter) and [OnExit](#onexit) interactions are applied to when they fire. Defaults to `Interactor`.

**Returns** \
[TargetEntity](../../../Murder/Utilities/TargetEntity.html) \

#### Kind

```csharp
public OnEnterOnExitKind Kind { get; init; }
```

Which kind of entity is allowed to trigger this area (and any extra behavior modifiers, such as skipping the enter interaction if an actor is already inside). Defaults to reacting only to the player.

**Returns** \
[OnEnterOnExitKind](../../../Murder/Components/Effects/OnEnterOnExitKind.html) \

#### TriggerOnLayer

```csharp
public readonly int? TriggerOnLayer;
```

Restricts triggering to entities on this specific collision layer, in addition to [Kind](#kind). Only applicable when non-player entities are allowed to trigger this area. `null` means no extra layer restriction is applied.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0)? \

⚡
