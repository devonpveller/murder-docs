# RenderedSpriteCacheComponent

**Namespace:** Murder.Components.Graphics \
**Assembly:** Murder.dll

```csharp
public sealed struct RenderedSpriteCacheComponent : IComponent
```

Runtime-only cache that stores the last fully resolved sprite rendering state for an entity, avoiding repeated lookups each frame.

**Intent:** Provide fast per-frame access to the calculated render parameters (position, animation frame, color, etc.) without recalculating them from scratch every tick.

**Use-case:** Added automatically by the sprite rendering system; read its properties when you need the entity's current rendered position, animation, or visual state from a system.

**Implements:** _[IComponent](../../../Bang/Components/IComponent.html)_

### ⭐ Properties
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


⚡