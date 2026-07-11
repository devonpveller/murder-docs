# OnEnterOnExitComponent

**Namespace:** Murder.Components.Effects \
**Assembly:** Murder.dll

```csharp
public sealed struct OnEnterOnExitComponent : IComponent
```

Triggers interaction callbacks when an entity enters or exits this entity's collision area.

**Implements:** _[IComponent](../../../Bang/Components/IComponent.html)_

**Intent:** Implements an area-trigger pattern by running `OnEnter` and `OnExit` interaction actions when a matching entity crosses the boundary.

**Use-case:** Attach to a trigger zone entity and configure `OnEnter`/`OnExit` with the desired `IInteractiveComponent` actions; the physics system fires these when the target entity type enters or leaves the collider.

### ⭐ Constructors
```csharp
public OnEnterOnExitComponent()
```

```csharp
public OnEnterOnExitComponent(IInteractiveComponent onEnter, IInteractiveComponent onExit)
```

**Parameters** \
`onEnter` [IInteractiveComponent](../../../Bang/Interactions/IInteractiveComponent.html) \
`onExit` [IInteractiveComponent](../../../Bang/Interactions/IInteractiveComponent.html) \

### ⭐ Properties
#### OnEnter
```csharp
public readonly IInteractiveComponent OnEnter;
```

Interaction to execute when a qualifying entity enters the trigger area.

**Returns** \
[IInteractiveComponent](../../../Bang/Interactions/IInteractiveComponent.html) \
#### OnExit
```csharp
public readonly IInteractiveComponent OnExit;
```

Interaction to execute when a qualifying entity leaves the trigger area.

**Returns** \
[IInteractiveComponent](../../../Bang/Interactions/IInteractiveComponent.html) \
#### Target
```csharp
public readonly TargetEntity Target;
```

Specifies which entity (interactor, parent, etc.) the interactions are applied to when triggered.

**Returns** \
[TargetEntity](../../../Murder/Utilities/TargetEntity.html) \


⚡