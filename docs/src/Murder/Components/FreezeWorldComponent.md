# FreezeWorldComponent

**Namespace:** Murder.Components \
**Assembly:** Murder.dll

```csharp
public sealed struct FreezeWorldComponent : IComponent
```

A unique, runtime-only component that requests a full pause of the world simulation, preventing all game systems from advancing until the freeze is released.

**Intent:** Pause all entity updates and physics simultaneously, for example during a hit-stop effect, a transition, or a UI pause menu.

**Use-case:** Add this component to the world entity (it is `[Unique]`) with the current game time as `StartTime`; multiple requestors increment `Count` so the world only resumes when the last request is removed.

**Implements:** _[IComponent](../../Bang/Components/IComponent.html)_

### ⭐ Constructors
```csharp
public FreezeWorldComponent(float startTime, int count)
```

**Parameters** \
`startTime` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`count` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

```csharp
public FreezeWorldComponent(float startTime)
```

**Parameters** \
`startTime` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

### ⭐ Properties
#### Count
```csharp
public readonly int Count;
```

Number of active freeze requests; the world stays frozen while this is greater than zero.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
#### StartTime
```csharp
public readonly float StartTime;
```

Absolute game time (in seconds) when the freeze was first requested, used to measure freeze duration.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \


⚡