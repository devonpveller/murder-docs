# TimeScaleComponent

**Namespace:** Murder.Components \
**Assembly:** Murder.dll

```csharp
public sealed struct TimeScaleComponent : IComponent
```

Applies a per-entity time scale multiplier that systems can use to speed up or slow down entity-specific logic independently of the global time scale.

**Intent:** Scale time locally for a single entity without affecting the rest of the world.

**Use-case:** Attach to an entity that should operate in slow-motion or fast-forward relative to other entities; systems that respect this component multiply their delta time by `Value` for that entity.

**Implements:** _[IComponent](../../Bang/Components/IComponent.html)_

### ⭐ Constructors
```csharp
public TimeScaleComponent(float scale)
```

**Parameters** \
`scale` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

### ⭐ Properties
#### Value
```csharp
public readonly float Value;
```

Time scale multiplier; 1.0 is normal speed, values below 1 slow the entity down, values above 1 speed it up.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \


⚡