# FreezeWorldComponent

**Namespace:** Murder.Components \
**Assembly:** Murder.dll

```csharp
public sealed struct FreezeWorldComponent : IComponent
```

Requests that the entire world simulation be paused. Used for effects such as hit-stop, transitions, or a pause menu, where gameplay systems should stop advancing but the pause itself may be requested by more than one source at a time (e.g. a cutscene and a menu opening simultaneously). It is `[Unique]`, so a single instance lives on the world; each requestor increments `Count` when adding it and decrements it when done, so the world only resumes once every requestor has released the freeze. Runtime-only: never persisted to save files.

**Intent:** Pause all entity updates and physics simultaneously, for example during a hit-stop effect, a transition, or a UI pause menu, while allowing multiple independent systems to request a freeze without stepping on each other.

**Use-case:** Add this component to the world entity (it is `[Unique]`) with the current game time as `StartTime`; multiple requestors increment `Count` so the world only resumes when the last request is removed. Use `FreezeWorldFlags.ShowUi` to keep UI updating/rendering during the freeze (e.g. for a pause menu) and `FreezeWorldFlags.AllowInputMessages` to still deliver input messages to entities while the rest of the world is frozen.

**Implements:** _[IComponent](../../Bang/Components/IComponent.html)_

### ⭐ Constructors

```csharp
public FreezeWorldComponent(float startTime)
```

Requests a world freeze starting at `startTime` with a single active request (`Count` = 1).

**Parameters** \
`startTime` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

```csharp
public FreezeWorldComponent(float startTime, int count)
```

Requests a world freeze starting at `startTime` with an explicit number of stacked requests.

**Parameters** \
`startTime` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`count` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

```csharp
public FreezeWorldComponent(float startTime, FreezeWorldFlags flags)
```

Requests a world freeze starting at `startTime` with the given behavior flags.

**Parameters** \
`startTime` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`flags` [FreezeWorldFlags](../../Murder/Components/FreezeWorldFlags.html) \

```csharp
public FreezeWorldComponent(float startTime, int count, FreezeWorldFlags flags)
```

Requests a world freeze starting at `startTime` with an explicit stacked request count and behavior flags.

**Parameters** \
`startTime` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`count` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`flags` [FreezeWorldFlags](../../Murder/Components/FreezeWorldFlags.html) \

### ⭐ Properties

#### Count

```csharp
public readonly int Count;
```

Number of active freeze requests. The world remains frozen while this is greater than zero; callers should increment it when stacking another freeze request and decrement it (or remove the component when it reaches zero) when their request is done.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### Flags

```csharp
public readonly FreezeWorldFlags Flags;
```

Flags controlling which systems keep running despite the freeze — see `FreezeWorldFlags`.

**Returns** \
[FreezeWorldFlags](../../Murder/Components/FreezeWorldFlags.html) \

#### ShowUi

```csharp
public readonly bool ShowUi { get; }
```

Whether UI should still be shown/updated while the world is frozen, derived from `FreezeWorldFlags.ShowUi`.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### StartTime

```csharp
public readonly float StartTime;
```

The game time (`Game.Now`) at which the freeze started, used to measure how long the world has been frozen.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

⚡
