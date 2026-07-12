# AnimationSpeedOverload

**Namespace:** Murder.Components \
**Assembly:** Murder.dll

```csharp
public sealed struct AnimationSpeedOverload : IComponent
```

Makes that the animation plays at a different rate.

**Implements:** _[IComponent](../../Bang/Components/IComponent.html)_

**Intent:** Overrides the playback speed of an entity's sprite animation, making it play faster or slower than its authored rate. `AgentSpriteSystem`/`RenderServices` read this alongside `AnimationOverloadComponent` to scale the animation's timing before drawing.

**Use-case:** Attach to slow down an animation during a slow-motion or hit-stop effect, or speed it up to match a gameplay state (e.g. a haste buff). `RenderServices.CompleteAnimationOverload` removes this component automatically once the current animation finishes **if `Persist` is `true`** — i.e. `Persist` marks the override as scoped to a single animation playthrough. Set `Persist` to `false` if the rate override should keep applying across subsequent animations until something else explicitly removes it.

### ⭐ Constructors

```csharp
public AnimationSpeedOverload(float rate, bool persist)
```

**Parameters** \
`rate` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`persist` [bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

### ⭐ Properties

#### Rate

```csharp
public readonly float Rate;
```

Playback speed multiplier; `1.0` is normal speed, `2.0` is double speed, `0.5` is half speed.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### Persist

```csharp
public readonly bool Persist;
```

When `true`, `RenderServices.CompleteAnimationOverload` removes this component the moment the currently playing animation completes — use this for a one-shot rate change tied to a single clip. When `false`, the override is left in place and keeps applying to subsequent animations until removed some other way.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

⚡
