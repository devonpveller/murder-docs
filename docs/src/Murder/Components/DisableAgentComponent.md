# DisableAgentComponent

**Namespace:** Murder.Components \
**Assembly:** Murder.dll

```csharp
public sealed struct DisableAgentComponent : IComponent
```

This will disable any conversion from impulse to velocity, or stopping velocity with friction. Effectively, this will pretend the entity doesn't have an [AgentComponent](../../Murder/Components/AgentComponent.html).

**Implements:** _[IComponent](../../Bang/Components/IComponent.html)_

**Intent:** Fully suspends `AgentMoverSystem`'s handling of the entity: impulses are no longer turned into velocity and friction is not applied, so whatever velocity the agent currently has is left untouched frame to frame. This is a harder stop than `AgentPauseRuntimeComponent`, which still applies friction so the agent gradually decelerates; use `DisableAgentComponent` when you want to directly control velocity yourself (e.g. a scripted knockback or a cutscene-driven slide) without the agent system fighting you.

**Use-case:** Add during cutscenes, dialogue, knockback, or any scripted movement where another system should own the entity's velocity outright. The `Count` field lets multiple independent systems request the disable without stepping on each other: call `Add()` when a new requester needs the agent disabled and `Remove()` when it's done; the component should only be removed from the entity once `Count` reaches zero, so the agent only resumes once every requester has released it.

### ⭐ Constructors

```csharp
public DisableAgentComponent()
```

Creates the component with a request count of `1`, the common case of a single system disabling the agent.

```csharp
public DisableAgentComponent(int count)
```

Creates the component with an explicit request count, typically used internally by `Add()`/`Remove()` to track multiple overlapping disable requests.

**Parameters** \
`count` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

### ⭐ Properties

#### Count

```csharp
public readonly int Count;
```

Number of independent requests currently disabling this agent. The entity should keep this component as long as `Count` is greater than zero, and only remove it once the last requester calls `Remove()` and it reaches zero.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

### ⭐ Methods

#### Add()

```csharp
public DisableAgentComponent Add()
```

Returns a new `DisableAgentComponent` with `Count` incremented by one, for use when another system needs to add its own request to keep the agent disabled.

**Returns** \
[DisableAgentComponent](../../Murder/Components/DisableAgentComponent.html) \

#### Remove()

```csharp
public DisableAgentComponent Remove()
```

Returns a new `DisableAgentComponent` with `Count` decremented by one. Callers should remove the component from the entity entirely once the returned `Count` reaches zero, allowing `AgentMoverSystem` to resume normal control.

**Returns** \
[DisableAgentComponent](../../Murder/Components/DisableAgentComponent.html) \

⚡
