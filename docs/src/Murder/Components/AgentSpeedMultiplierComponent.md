# AgentSpeedMultiplierComponent

**Namespace:** Murder.Components \
**Assembly:** Murder.dll

```csharp
public sealed struct AgentSpeedMultiplierComponent : IComponent
```

Holds an array of per-slot speed multipliers applied on top of the agent's base speed.

**Implements:** _[IComponent](../../Bang/Components/IComponent.html)_

**Intent:** Allows multiple independent systems to each apply a fractional speed modifier to an agent without overwriting one another.

**Use-case:** A status-effect system sets slot 0 to `0.5` to halve the agent's speed; another system sets slot 1 to `0.8` for a second debuff — `AgentMoverSystem` multiplies its base `agent.Speed` by every slot's value each frame (see `GetVelocity` in `AgentMoverSystem`), so independent systems can each own a dedicated slot without clobbering each other. The type is marked `[RuntimeOnly]` and `[DoNotPersistOnSave]`, so it is never saved to disk — it exists purely as transient runtime state that must be re-applied by whatever system owns each slot.

### ⭐ Constructors

```csharp
public AgentSpeedMultiplierComponent(int slot, float speedMultiplier)
```

Creates a component with `speedMultiplier` written into `slot` and all other slots set to `1.0` (no modification). Note this constructor always starts from the neutral 8-slot template, so it is only suitable when you are setting a single slot; to combine multiple active slots, read the existing component with `TryGetAgentSpeedMultiplier`, copy `SpeedMultiplier`, and write the desired index yourself.

**Parameters** \
`slot` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`speedMultiplier` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

### ⭐ Properties

#### \_emptyTemplate

```csharp
public static readonly ImmutableArray<float> _emptyTemplate;
```

Shared 8-slot template with every value initialized to `1.0`, used internally as the starting point when the single-slot constructor builds a new component.

**Returns** \
[ImmutableArray\<float\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \

#### SpeedMultiplier

```csharp
public readonly ImmutableArray<float> SpeedMultiplier { get; public set; }
```

Array of 8 independent speed multiplier slots. `AgentMoverSystem` multiplies all 8 values together (starting from `1.0`) to compute the final speed multiplier applied on top of `AgentComponent.Speed`; a slot value below `1.0` slows the agent, above `1.0` speeds it up, and `1.0` is a no-op.

**Returns** \
[ImmutableArray\<float\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \

⚡
