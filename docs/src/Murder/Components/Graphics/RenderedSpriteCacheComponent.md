# RenderedSpriteCacheComponent

**Namespace:** Murder.Components.Graphics \
**Assembly:** Murder.dll

```csharp
public sealed struct RenderedSpriteCacheComponent : IComponent, IModifiableComponent, IDoNotCheckOnReplaceTag
```

Runtime-only cache that stores the last fully resolved sprite rendering state for an entity (position, animation, color, blend, outline, etc.), so other systems can read "what did this entity actually look like last frame" without recomputing it from `SpriteComponent`, `TintComponent`, `ScaleComponent`, and friends. `RenderServices.UpdateRenderedSpriteCache` writes to it once per frame from `SpriteRenderSystem`, `SpriteAtRatioRenderSystem`, and `AgentSpriteSystem` after they finish resolving a sprite's draw parameters.

**Intent:** Avoid both the cost of recomputing render state and the cost of a full `Entity.ReplaceComponent` every single frame. The component wraps its data in a small mutable reference class (`RenderedSpriteReference`) instead of storing the values directly as `readonly` fields; combined with `IDoNotCheckOnReplaceTag` (which skips the equality check `ReplaceComponent` would otherwise do) and a set of read-only computed properties that proxy straight to `Ref.Cache`, this lets `RenderServices.UpdateRenderedSpriteCache` mutate `Ref.Cache` in place on subsequent frames instead of allocating and replacing the component each time. It also implements `IModifiableComponent` because that interface is required to opt out of Bang's normal by-value component semantics, but its `Subscribe`/`Unsubscribe` are deliberately empty ("don't support") — nothing actually needs to be notified when the cache silently updates.

**Use-case:** Never construct or mutate this directly from gameplay code; it is entirely owned by the sprite-rendering systems. Read it (e.g. via `entity.TryGetRenderedSpriteCache()` or `entity.GetRenderedSpriteCache()`) from other systems when you need to know the entity's most recently rendered position, current animation, sorting value, or visual state — for example `AgentSpriteSystem` reads `AnimInfo.Name` from it to detect whether the animation actually changed before deciding to trigger a "force animation on chance" roll.

**Implements:** _[IComponent](../../../Bang/Components/IComponent.html), [IModifiableComponent](../../../Bang/Components/IModifiableComponent.html), [IDoNotCheckOnReplaceTag](../../../Bang/Components/IDoNotCheckOnReplaceTag.html)_

### ⭐ Constructors

```csharp
public RenderedSpriteCacheComponent()
```

Creates an empty cache backed by a fresh, default-valued [RenderedSpriteCache](../../../Murder/Components/Graphics/RenderedSpriteCache.html). This is what `Entity.SetRenderedSpriteCache` uses the first time the component is attached to an entity.

```csharp
public RenderedSpriteCacheComponent(RenderedSpriteCache cache)
```

Creates a cache pre-populated with the given [RenderedSpriteCache](../../../Murder/Components/Graphics/RenderedSpriteCache.html) snapshot.

**Parameters** \
`cache` [RenderedSpriteCache](../../../Murder/Components/Graphics/RenderedSpriteCache.html) \

### ⭐ Properties

#### Ref

```csharp
public readonly RenderedSpriteReference Ref;
```

The mutable [RenderedSpriteReference](../../../Murder/Components/Graphics/RenderedSpriteReference.html) box holding the actual cached data. `RenderServices.UpdateRenderedSpriteCache` mutates `Ref.Cache` in place on this shared instance so the render systems can refresh the cache every frame without replacing the component or triggering entity-modified notifications.

**Returns** \
[RenderedSpriteReference](../../../Murder/Components/Graphics/RenderedSpriteReference.html) \

#### AnimInfo

```csharp
public AnimationInfo AnimInfo { get; public set; }
```

Cached animation metadata for the currently playing animation sequence.

**Returns** \
[AnimationInfo](../../../Murder/Core/Graphics/AnimationInfo.html) \

#### Blend

```csharp
public BlendStyle Blend { get; public set; }
```

Blend mode used when drawing the sprite (e.g. normal, additive).

**Returns** \
[BlendStyle](../../../Murder/Core/Graphics/BlendStyle.html) \

#### Color

```csharp
public Color Color { get; public set; }
```

Color tint applied to the sprite when it was last rendered.

**Returns** \
[Color](../../../Murder/Core/Graphics/Color.html) \

#### CurrentAnimation

```csharp
public Animation CurrentAnimation { get; public set; }
```

The animation object that is currently playing on the entity.

**Returns** \
[Animation](../../../Murder/Core/Graphics/Animation.html) \

#### ImageFlip

```csharp
public ImageFlip ImageFlip { get; public set; }
```

Horizontal or vertical flip applied to the rendered sprite.

**Returns** \
[ImageFlip](../../../Murder/Core/Graphics/ImageFlip.html) \

#### LastFrameIndex

```csharp
public int LastFrameIndex { get; public set; }
```

The last recorded animation frame. Uses the internal animation frame index (as tracked by the animation evaluator), not the generic/public frame index exposed elsewhere — compare frame-to-frame to detect when the sprite actually advanced to a new frame.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### Offset

```csharp
public Vector2 Offset { get; public set; }
```

Pixel offset applied to the sprite's drawn position relative to the entity's world position.

**Returns** \
[Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

#### Outline

```csharp
public OutlineStyle Outline { get; public set; }
```

Outline style drawn around the sprite edges.

**Returns** \
[OutlineStyle](../../../Murder/Core/Graphics/OutlineStyle.html) \

#### RenderedSprite

```csharp
public Guid RenderedSprite { get; public set; }
```

GUID of the sprite asset that was last rendered for this entity.

**Returns** \
[Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \

#### RenderPosition

```csharp
public Vector2 RenderPosition { get; public set; }
```

Final screen-space position at which the sprite was drawn in the last frame.

**Returns** \
[Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

#### Rotation

```csharp
public float Rotation { get; public set; }
```

Rotation angle (in radians) applied to the sprite when it was last rendered.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### Scale

```csharp
public Vector2 Scale { get; public set; }
```

Scale factor applied to the sprite when it was last rendered.

**Returns** \
[Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

#### Sorting

```csharp
public float Sorting { get; public set; }
```

Draw-order sorting value used to determine the render layer of the sprite.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### SpriteSize

```csharp
public Point SpriteSize { get; public set; }
```

Pixel dimensions of the sprite asset that was last rendered, as read from the resolved `SpriteAsset`.

**Returns** \
[Point](../../../Murder/Core/Geometry/Point.html) \

### ⭐ Methods

#### Subscribe(Action)

```csharp
public void Subscribe(Action notification)
```

Required by [IModifiableComponent](../../../Bang/Components/IModifiableComponent.html), but intentionally a no-op ("don't support") — nothing needs to observe when this cache is refreshed, so no callback is ever stored or invoked.

**Parameters** \
`notification` [Action](https://learn.microsoft.com/en-us/dotnet/api/System.Action?view=net-7.0) \

#### Unsubscribe(Action)

```csharp
public void Unsubscribe(Action notification)
```

Required by [IModifiableComponent](../../../Bang/Components/IModifiableComponent.html); like `Subscribe`, intentionally a no-op.

**Parameters** \
`notification` [Action](https://learn.microsoft.com/en-us/dotnet/api/System.Action?view=net-7.0) \

⚡
