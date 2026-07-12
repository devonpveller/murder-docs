# SpriteBlendComponent

**Namespace:** Murder.Components.Graphics \
**Assembly:** Murder.dll

```csharp
public sealed struct SpriteBlendComponent : IComponent
```

Overrides how an entity's sprite is blended into the frame buffer.

**Intent:** Let specific entities opt into a non-default blend mode (e.g. additive glow, or a custom `MurderBlendState`) without changing the render system itself. `SpriteRenderSystem` and `AgentSpriteSystem` both read it the same way: they start from `BlendStyle.Normal` (or `BlendStyle.Wash` while the entity has a [FlashSpriteComponent](../../../Murder/Components/FlashSpriteComponent.html)) and `MurderBlendState.AlphaBlend`, then override the style with `BlendStyle` when it is non-null and always take `BlendState` from this component when present.

**Use-case:** Add to a sprite entity that needs a special blend mode — for example an additive-blended particle-like effect sprite, or a sprite that must ignore the destination alpha channel — by providing an explicit `BlendStyle` and `BlendState`. Leave `BlendStyle` `null` (the default) to keep automatic style selection (including the flash-hit wash effect) while still overriding just the graphics-device `BlendState`.

**Implements:** _[IComponent](../../../Bang/Components/IComponent.html)_

### ⭐ Constructors

```csharp
public SpriteBlendComponent()
```

Creates a blend override with no style override (`BlendStyle = null`) and the default `MurderBlendState.AlphaBlend` state — equivalent to normal rendering.

```csharp
public SpriteBlendComponent(BlendStyle blendStyle, MurderBlendState blendState)
```

**Parameters** \
`blendStyle` [BlendStyle](../../../Murder/Core/Graphics/BlendStyle.html) \
`blendState` [MurderBlendState](../../../Murder/Core/Graphics/MurderBlendState.html) \

### ⭐ Properties

#### BlendState

```csharp
public readonly MurderBlendState BlendState;
```

Graphics-device blend state (how source and destination color/alpha are combined) applied when drawing the sprite.

**Returns** \
[MurderBlendState](../../../Murder/Core/Graphics/MurderBlendState.html) \

#### BlendStyle

```csharp
public readonly BlendStyle? BlendStyle;
```

When set, overrides the shader-level blend style that would otherwise be derived automatically (e.g. the flash-hit wash effect). `null` leaves the automatic style selection in place.

**Returns** \
[BlendStyle](../../../Murder/Core/Graphics/BlendStyle.html)? \

⚡
