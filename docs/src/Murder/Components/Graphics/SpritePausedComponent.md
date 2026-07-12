# SpritePausedComponent

**Namespace:** Murder.Components.Graphics \
**Assembly:** Murder.dll

```csharp
public sealed struct SpritePausedComponent : IComponent
```

Runtime-only marker that freezes an agent's sprite animation at a fixed point in time.

**Intent:** Give gameplay code a way to pause an individual agent's animation (e.g. while a character is stunned, in a cutscene beat, or waiting on a scripted trigger) without having to remove or replace its `AgentSpriteComponent`/`SpriteComponent`. `AgentSpriteSystem` checks for this component and, when present, sets `AnimationInfo.OverrideCurrentTime` to `PausedAt`, so the animation evaluator always renders the frame corresponding to that fixed time instead of advancing.

**Use-case:** Add via `entity.SetSpritePaused()` (using the default constructor, which stamps the current `Game.Now`) to freeze an agent's animation right now, or with an explicit time to freeze it at a specific moment. Remove the component to resume normal playback. Note this only affects agent-driven sprites processed by `AgentSpriteSystem`; for a general-purpose "pause this animation" marker outside of the agent pipeline, see [PauseAnimationComponent](../../../Murder/Components/PauseAnimationComponent.html), which instead keeps the animation running on unscaled time.

**Implements:** _[IComponent](../../../Bang/Components/IComponent.html)_

### ⭐ Constructors

```csharp
public SpritePausedComponent()
```

Creates a pause marker stamped with the current game time (`Game.Now`).

```csharp
public SpritePausedComponent(float pausedAt)
```

**Parameters** \
`pausedAt` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

### ⭐ Properties

#### PausedAt

```csharp
public readonly float PausedAt;
```

Absolute game time at which the animation was paused; the animation is evaluated as if time were frozen at this value.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

⚡
