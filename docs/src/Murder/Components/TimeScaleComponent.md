# TimeScaleComponent

**Namespace:** Murder.Components \
**Assembly:** Murder.dll

```csharp
public sealed struct TimeScaleComponent : IComponent
```

Contributes a multiplicative factor to the game's global time scale.

**Intent:** Let gameplay code drive the game's overall speed (e.g. a bullet-time or hit-pause effect) declaratively, by attaching a component instead of writing directly to the game's time-scale state.

**Use-case:** Attach to any entity — typically a dedicated, otherwise-empty controller entity — to slow down or speed up the entire game. This is **not** a per-entity scale: `TimeScaleSystem` multiplies together the `Value` of every entity currently carrying this component to compute the game's single global time scale, so if more than one entity has it attached simultaneously their values combine. Remove the component (or the entity) to remove its contribution; when the last one is removed the global time scale returns to `1`.

**Implements:** _[IComponent](../../Bang/Components/IComponent.html)_

### ⭐ Constructors

```csharp
public TimeScaleComponent(float scale)
```

Creates a component contributing `scale` to the global time scale.

**Parameters** \
`scale` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

### ⭐ Properties

#### Value

```csharp
public readonly float Value;
```

Multiplier this entity contributes to the global time scale; `1.0` is normal speed, values below `1` slow the whole game down, values above `1` speed it up. Combined multiplicatively with the `Value` of every other entity carrying this component.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

⚡
