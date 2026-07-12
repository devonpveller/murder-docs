# TweenSystem

**Namespace:** Murder.Systems \
**Assembly:** Murder.dll

```csharp
public class TweenSystem : IUpdateSystem, ISystem
```

Updates entities with `TweenComponent` each frame, evaluating position and scale curves at the current eased progress and removing the component when the animation completes.

**Intent:** Drives component-based property tweening (position and scale) for entities, cleaning itself up when the animation is done.

**Use-case:** Add `TweenComponent` to any entity that needs a timed interpolation of its position or scale; no callbacks or manual removal are required.

**Implements:** _[IUpdateSystem](../../Bang/Systems/IUpdateSystem.html), [ISystem](../../Bang/Systems/ISystem.html)_

### ⭐ Constructors

```csharp
public TweenSystem()
```

### ⭐ Methods

#### Update(Context)

```csharp
public virtual void Update(Context context)
```

Evaluates the tween's easing function at the current elapsed time and applies interpolated position and scale values to the entity; removes `TweenComponent` on completion.

**Parameters** \
`context` [Context](../../Bang/Contexts/Context.html) \

⚡
