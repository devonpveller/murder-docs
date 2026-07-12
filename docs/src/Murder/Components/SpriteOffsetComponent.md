# SpriteOffsetComponent

**Namespace:** Murder.Components \
**Assembly:** Murder.dll

```csharp
public sealed struct SpriteOffsetComponent : IComponent
```

Applies a world-space pixel offset to the entity's sprite rendering position, decoupling the visual position from the logical entity position.

**Intent:** Nudge the rendered sprite relative to the entity's transform without moving the entity itself.

**Use-case:** Attach when a sprite's pivot or visual center doesn't align with the entity's logical origin, or for animation-driven positional offsets. `SpriteRenderSystem` and `AgentSpriteSystem` both check for it (`e.TryGetSpriteOffset()`) and add `Offset` directly to the computed render position after any `SpriteClippingRectComponent` offset has already been applied, so it stacks cleanly with other rendering-position adjustments.

**Implements:** _[IComponent](../../Bang/Components/IComponent.html)_

### ⭐ Constructors

```csharp
public SpriteOffsetComponent(float x, float y)
```

**Parameters** \
`x` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`y` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

```csharp
public SpriteOffsetComponent(Vector2 offset)
```

**Parameters** \
`offset` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

### ⭐ Properties

#### Offset

```csharp
public readonly Vector2 Offset;
```

Pixel offset in world space added to the entity's position before rendering the sprite.

**Returns** \
[Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

⚡
