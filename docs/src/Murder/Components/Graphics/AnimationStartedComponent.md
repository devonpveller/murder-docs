# AnimationStartedComponent

**Namespace:** Murder.Components.Graphics \
**Assembly:** Murder.dll

```csharp
public sealed struct AnimationStartedComponent : IComponent
```

Runtime-only marker recording the game time at which the current animation began playing on the entity. Marked with `[RuntimeOnly, DoNotPersistOnSave]`, so it is never written to save data or serialized assets.

**Intent:** Give the render pipeline a stable "animation start" timestamp to evaluate against, instead of recomputing it every frame. Without this component the animation's elapsed time would be ambiguous the moment more than one system reads it in the same frame.

**Use-case:** `SpriteAnimationStarterSystem` adds this to every entity with a `SpriteComponent` that doesn't have it yet, stamping `StartTime` with `Game.Now` (or `Game.UnscaledDeltaTime` when `SpriteComponent.UseUnscaledTime` is set) right before rendering. `SpriteRenderSystem` then reads it via `TryGetAnimationStarted()` to know exactly when the current animation began. Game code rarely needs to add or read this directly; it is removed automatically whenever a new animation is queued (e.g. by `EntityServices.PlaySpriteAnimationOnce`/`TryPlaySpriteAnimation`) so a fresh start time gets stamped the next frame.

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
