# AgentSpeedMultiplierComponent

**Namespace:** Murder.Components \
**Assembly:** Murder.dll

```csharp
public sealed struct AgentSpeedMultiplierComponent : IComponent
```

Holds an array of per-slot speed multipliers applied on top of the agent's base speed.

**Implements:** _[IComponent](../../Bang/Components/IComponent.html)_

**Intent:** Allows multiple independent systems to each apply a fractional speed modifier to an agent without overwriting one another.

**Use-case:** A status-effect system sets slot 0 to `0.5` to halve the agent's speed; another system sets slot 1 to `0.8` for a second debuff — the final speed is the product of all slot values multiplied by the base speed.

### ⭐ Constructors
```csharp
public AgentSpeedMultiplierComponent(int slot, float speedMultiplier)
```

Creates a component with `speedMultiplier` written into `slot` and all other slots set to `1.0`.

**Parameters** \
`slot` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`speedMultiplier` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

### ⭐ Properties
#### _emptyTemplate
```csharp
public readonly static ImmutableArray<T> _emptyTemplate;
```

Default template with all 8 multiplier slots initialized to `1.0` (no modification).

**Returns** \
[ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \
#### SpeedMultiplier
```csharp
public ImmutableArray<T> SpeedMultiplier { get; public set; }
```

Array of speed multiplayers, Currentlty with 8 slots

**Returns** \
[ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \


⚡