# PolygonSpriteRenderSystem

**Namespace:** Murder.Systems \
**Assembly:** Murder.dll

```csharp
public class PolygonSpriteRenderSystem : IMurderRenderSystem, IRenderSystem, ISystem
```

Renders polygon-shaped sprites (currently circles) defined in a `PolygonSpriteComponent` to the scene's sprite batch with y-sorting.

**Intent:** Draws procedural filled shapes at an entity's world position as an alternative to texture-based sprites.

**Use-case:** Attach `PolygonSpriteComponent` to entities that need simple filled shapes; available in editor by default.

**Implements:** _[IMurderRenderSystem](../../Murder/Core/Graphics/IMurderRenderSystem.html), [IRenderSystem](../../Bang/Systems/IRenderSystem.html), [ISystem](../../Bang/Systems/ISystem.html)_

### ⭐ Constructors

```csharp
public PolygonSpriteRenderSystem()
```

### ⭐ Methods

#### Draw(RenderContext, Context)

```csharp
public virtual void Draw(RenderContext render, Context context)
```

Iterates entities with `PolygonSpriteComponent` and draws each declared shape (circle, etc.) at the entity's world position with color and y-sort offset applied.

**Parameters** \
`render` [RenderContext](../../Murder/Core/Graphics/RenderContext.html) \
`context` [Context](../../Bang/Contexts/Context.html) \

⚡
