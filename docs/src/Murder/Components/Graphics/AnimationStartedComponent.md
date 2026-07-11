# AnimationStartedComponent

**Namespace:** Murder.Components.Graphics \
**Assembly:** Murder.dll

```csharp
public sealed struct AnimationStartedComponent : IComponent
```

Runtime-only marker recording the game time at which the current animation began playing on the entity.

**Intent:** Track when an animation was started so that systems can compute elapsed time, synchronize events, or detect animation restarts.

**Use-case:** Added automatically by the animation system when a new animation sequence begins; read `StartTime` to calculate how far into the animation the entity currently is.

**Implements:** _[IComponent](../../../Bang/Components/IComponent.html)_

### ⭐ Constructors
```csharp
public AnimationStartedComponent(float startTime)
```

**Parameters** \
`startTime` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

### ⭐ Properties
#### StartTime
```csharp
public readonly float StartTime;
```

Absolute game time (in seconds) when the current animation started playing.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \


⚡