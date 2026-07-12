# HighlightSpriteComponent

**Namespace:** Murder.Components \
**Assembly:** Murder.dll

```csharp
public sealed struct HighlightSpriteComponent : IComponent
```

Causes an entity's sprite to be rendered with a solid-color outline, used to visually call out interactable or targeted entities. Read by `SpriteRenderSystem` to set the sprite's outline color (unless a `DeactivateHighlightSpriteComponent` is also present, which suppresses the outline).

**Intent:** Draw attention to an interactable or selected entity by rendering a colored outline over its sprite, without needing a separate overlay entity or shader per case.

**Use-case:** Prefer calling `EffectsServices.ApplyHighlight`/`EffectsServices.RemoveHighlight` rather than setting this component directly — those helpers also honor `HighlightOnChildrenComponent` to redirect the highlight to the entity's children when appropriate. Provide the desired `Color` (e.g. when the player hovers over or targets an entity), and remove the component (or call `RemoveHighlight`) to clear it.

**Implements:** _[IComponent](../../Bang/Components/IComponent.html)_

### ⭐ Constructors

```csharp
public HighlightSpriteComponent(Color color)
```

Highlights the sprite with the given outline `color`.

**Parameters** \
`color` [Color](../../Murder/Core/Graphics/Color.html) \

### ⭐ Properties

#### Color

```csharp
public readonly Color Color;
```

Outline color drawn around the sprite while highlighted (default is white).

**Returns** \
[Color](../../Murder/Core/Graphics/Color.html) \

⚡
