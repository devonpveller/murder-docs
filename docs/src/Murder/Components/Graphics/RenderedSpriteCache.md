# RenderedSpriteCache

**Namespace:** Murder.Components.Graphics \
**Assembly:** Murder.dll

```csharp
public sealed struct RenderedSpriteCache
```

Immutable snapshot of everything needed to describe how an entity's sprite was drawn on a given frame: resolved position, animation, transform, color, and render metadata.

**Intent:** Produced by the sprite render systems (`SpriteRenderSystem`, `SpriteAtRatioRenderSystem`, `AgentSpriteSystem`) after they finish resolving a sprite's draw parameters for the frame, and stored via [RenderedSpriteReference](../../../Murder/Components/Graphics/RenderedSpriteReference.html) on [RenderedSpriteCacheComponent](../../../Murder/Components/Graphics/RenderedSpriteCacheComponent.html). Keeping this as a plain value type (rather than mutating fields piecemeal) means each frame's cache update is built with `with`-expressions (`new RenderedSpriteCache() with { ... }`) from a clean snapshot, so partially-updated/inconsistent states can't leak between systems.

**Use-case:** Read (never construct directly outside the render systems) via `RenderedSpriteCacheComponent`'s properties when another system needs to know an entity's last rendered position, current animation, or visual state — for example, `RenderServices.TriggerEventsIfNeeded` compares the new frame against `LastFrameIndex` here to know whether an animation actually advanced before firing frame events.

### ⭐ Properties

#### AnimInfo

```csharp
public AnimationInfo AnimInfo { get; init; }
```

Animation metadata (name, start time, loop flag) for the currently playing animation.

**Returns** \
[AnimationInfo](../../../Murder/Core/Graphics/AnimationInfo.html) \

#### Blend

```csharp
public BlendStyle Blend { get; init; }
```

Blend mode used when drawing the sprite.

**Returns** \
[BlendStyle](../../../Murder/Core/Graphics/BlendStyle.html) \

#### Color

```csharp
public Color Color { get; init; }
```

Color tint applied to the sprite.

**Returns** \
[Color](../../../Murder/Core/Graphics/Color.html) \

#### CurrentAnimation

```csharp
public Animation CurrentAnimation { get; init; }
```

The animation object that was rendered.

**Returns** \
[Animation](../../../Murder/Core/Graphics/Animation.html) \

#### ImageFlip

```csharp
public ImageFlip ImageFlip { get; init; }
```

Horizontal or vertical flip applied to the rendered sprite.

**Returns** \
[ImageFlip](../../../Murder/Core/Graphics/ImageFlip.html) \

#### LastFrameIndex

```csharp
public int LastFrameIndex { get; init; }
```

The last recorded animation frame. Uses the internal animation frame index, not the generic/public frame index.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### Offset

```csharp
public Vector2 Offset { get; init; }
```

Pixel offset applied to the sprite's drawn position relative to the entity's world position.

**Returns** \
[Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

#### Outline

```csharp
public OutlineStyle Outline { get; init; }
```

Outline style drawn around the sprite edges.

**Returns** \
[OutlineStyle](../../../Murder/Core/Graphics/OutlineStyle.html) \

#### RenderedSprite

```csharp
public Guid RenderedSprite { get; init; }
```

GUID of the sprite asset that was rendered.

**Returns** \
[Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \

#### RenderPosition

```csharp
public Vector2 RenderPosition { get; init; }
```

Final screen-space position at which the sprite was drawn.

**Returns** \
[Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

#### Rotation

```csharp
public float Rotation { get; init; }
```

Rotation angle (in radians) applied to the sprite.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### Scale

```csharp
public Vector2 Scale { get; init; }
```

Scale factor applied to the sprite.

**Returns** \
[Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

#### Sorting

```csharp
public float Sorting { get; init; }
```

Draw-order sorting value used to determine the render layer of the sprite.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### SpriteSize

```csharp
public Point SpriteSize { get; init; }
```

Pixel dimensions of the rendered sprite asset.

**Returns** \
[Point](../../../Murder/Core/Geometry/Point.html) \

⚡
