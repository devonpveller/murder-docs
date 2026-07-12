# FlipSpriteComponent

**Namespace:** Murder.Components.Graphics \
**Assembly:** Murder.dll

```csharp
public sealed struct FlipSpriteComponent : IComponent
```

Mirrors an entity's sprite horizontally and/or vertically at draw time, without modifying the source asset.

**Intent:** Let a single sprite asset be reused facing either direction (or upside-down) instead of authoring mirrored duplicates. `SpriteRenderSystem` reads `Orientation` and passes it straight through to the draw call; `DynamicInCameraSystem` also factors it into the on-screen bounding box it computes for camera-visibility culling, so a flipped sprite's origin/offset is accounted for correctly.

**Use-case:** Add via `EffectsServices.CreateQuickSprite` (which takes a `QuickSpriteInfo.Flip`) to spawn a one-shot effect facing a particular direction, or set/toggle it from editor tooling such as `EntitiesShortcutsSystem`'s sprite-flip shortcuts. For agents whose facing changes dynamically at runtime based on movement direction, prefer [SpriteFacingComponent](../../../Murder/Components/SpriteFacingComponent.html) (which can flip per angle-slice) over manually managing this component.

**Implements:** _[IComponent](../../../Bang/Components/IComponent.html)_

### ⭐ Constructors

```csharp
public FlipSpriteComponent(ImageFlip flip)
```

**Parameters** \
`flip` [ImageFlip](../../../Murder/Core/Graphics/ImageFlip.html) \

### ⭐ Properties

#### Orientation

```csharp
public readonly ImageFlip Orientation;
```

Which axis (or axes) the sprite is flipped on.

**Returns** \
[ImageFlip](../../../Murder/Core/Graphics/ImageFlip.html) \

⚡
