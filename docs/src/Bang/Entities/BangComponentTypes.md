# BangComponentTypes

**Namespace:** Bang.Entities \
**Assembly:** Bang.dll

```csharp
public static class BangComponentTypes
```

Ids reserved for special Bang components.

Every component type gets a unique integer index from the world's `ComponentsLookup`, and [Entity](../../Bang/Entities/Entity.html) uses that index (not the `Type` itself) internally for all of its component storage and lookups — see `Entity.HasComponent(int)`, `Entity.AddComponent(T, int)`, etc. Most indices are assigned dynamically per-project by the source generator (see [MurderComponentTypes](../../Bang/Entities/MurderComponentTypes.html)), but the three components that Bang's core engine itself depends on — [IStateMachineComponent](../../Bang/StateMachines/IStateMachineComponent.html), [IInteractiveComponent](../../Bang/Interactions/IInteractiveComponent.html) and [PositionComponent](../Components/PositionComponent.html) — are pinned to fixed, well-known indices instead, since Bang code needs to reference them without depending on any particular project's generated lookup. This class simply exposes those three constants. Application code should not normally need these directly: use the strongly-typed helpers in [Extensions](../../Bang/Entities/Extensions.html) (e.g. `entity.HasStateMachine()`, `entity.GetPosition()`) instead of comparing against `BangComponentTypes.*` by hand.

### ⭐ Properties
#### Interactive
```csharp
public static const int Interactive;
```

Unique Id used for the lookup of components with type [IInteractiveComponent](../../Bang/Interactions/IInteractiveComponent.html).

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
#### Position
```csharp
public static const int Position;
```

Unique Id used for the lookup of components with type [PositionComponent](../Components/PositionComponent.html).

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
#### StateMachine
```csharp
public static const int StateMachine;
```

Unique Id used for the lookup of components with type [IStateMachineComponent](../../Bang/StateMachines/IStateMachineComponent.html).

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \


⚡