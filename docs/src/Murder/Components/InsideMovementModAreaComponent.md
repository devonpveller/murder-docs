# InsideMovementModAreaComponent

**Namespace:** Murder.Components \
**Assembly:** Murder.dll

```csharp
public sealed struct InsideMovementModAreaComponent : IComponent
```

Runtime component that tracks all movement-modifier areas the entity is currently overlapping, aggregating their speed and slide effects.

**Intent:** Record that an agent is inside one or more `MovementModAreaComponent` zones so the movement system can apply the combined speed multiplier and slide vector each frame.

**Use-case:** Added and removed automatically by the `AgentMovementModifierSystem`; read `areas` in the movement system to apply all active movement modifiers to the agent's velocity.

**Implements:** _[IComponent](../../Bang/Components/IComponent.html)_

### ⭐ Constructors
```csharp
public InsideMovementModAreaComponent(MovementModAreaComponent area)
```

**Parameters** \
`area` [MovementModAreaComponent](../../Murder/Components/MovementModAreaComponent.html) \

```csharp
public InsideMovementModAreaComponent(ImmutableArray<T> areas)
```

**Parameters** \
`areas` [ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \

### ⭐ Properties
#### areas
```csharp
public readonly ImmutableArray<T> areas;
```

List of all movement-modifier area infos the entity is currently inside, each describing the originating area entity and its movement parameters.

**Returns** \
[ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \
### ⭐ Methods
#### AddArea(MovementModAreaComponent)
```csharp
public InsideMovementModAreaComponent AddArea(MovementModAreaComponent area)
```

Returns a new component that includes the given area, or the same component unchanged if the area is already tracked.

**Parameters** \
`area` [MovementModAreaComponent](../../Murder/Components/MovementModAreaComponent.html) \

**Returns** \
[InsideMovementModAreaComponent](../../Murder/Components/InsideMovementModAreaComponent.html) \



⚡