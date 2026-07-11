# HighlightSpriteComponent

**Namespace:** Murder.Components \
**Assembly:** Murder.dll

```csharp
public sealed struct HighlightSpriteComponent : IComponent
```

Causes the entity's sprite to be drawn with a solid color overlay, visually highlighting it.

**Intent:** Draw attention to an interactable or selected entity by rendering a colored highlight over its sprite.

**Use-case:** Add when the player hovers over or targets an entity and provide the desired `Color`; remove the component to clear the highlight.

**Implements:** _[IComponent](../../Bang/Components/IComponent.html)_

### ⭐ Constructors
```csharp
public HighlightSpriteComponent(Color color)
```

**Parameters** \
`color` [Color](../../Murder/Core/Graphics/Color.html) \

### ⭐ Properties
#### Color
```csharp
public readonly Color Color;
```

Color of the highlight overlay drawn on top of the sprite (default is white).

**Returns** \
[Color](../../Murder/Core/Graphics/Color.html) \


⚡