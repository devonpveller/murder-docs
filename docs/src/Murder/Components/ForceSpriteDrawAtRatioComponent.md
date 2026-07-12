# ForceSpriteDrawAtRatioComponent

**Namespace:** Murder.Components \
**Assembly:** Murder.dll

```csharp
public sealed struct ForceSpriteDrawAtRatioComponent : IComponent
```

Drives an entity's sprite animation directly from a normalized 0-1 progress value instead of elapsed game time.

**Intent:** Entities with this component are filtered out of the normal `SpriteRenderSystem` (`[Filter(ContextAccessorFilter.NoneOf, typeof(ForceSpriteDrawAtRatioComponent), ...)]`) and instead handled by `SpriteAtRatioRenderSystem`, which maps `Ratio` onto the current animation's frame range via `Batch2D.DrawSpriteAtRatio`. It also passes `AnimationEventsTriggerFlag.AllowReverse` when firing frame events, so animation events still trigger correctly even if `Ratio` decreases between frames.

**Use-case:** Add to a sprite entity whose animation should be scrubbed explicitly by some other piece of state — for example, tying a sprite's frame to a loading bar, a charge/cooldown meter, or a health bar's fill animation — rather than letting it play back automatically over time. Set `Ratio` every frame (or whenever the driving value changes) to the desired 0 (first frame) to 1 (last frame) progress.

**Implements:** _[IComponent](../../Bang/Components/IComponent.html)_

### ⭐ Constructors

```csharp
public ForceSpriteDrawAtRatioComponent()
```

Creates a ratio override starting at 0 (first frame).

```csharp
public ForceSpriteDrawAtRatioComponent(float ratio)
```

**Parameters** \
`ratio` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

### ⭐ Properties

#### Ratio

```csharp
public readonly float Ratio;
```

Normalized progress (0 = first frame, 1 = last frame) through the current animation.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

⚡
