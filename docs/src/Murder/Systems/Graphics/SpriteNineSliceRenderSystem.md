# SpriteNineSliceRenderSystem

**Namespace:** Murder.Systems.Graphics \
**Assembly:** Murder.dll

```csharp
public class SpriteNineSliceRenderSystem : IMurderRenderSystem, IRenderSystem, ISystem
```

Draws every visible entity with a [NineSliceComponent](../../../Murder/Components/NineSliceComponent.html) by stretching only the interior regions of its source sprite to fill `NineSliceComponent.Target`, keeping the corners and edges undistorted. This is the standard way to render resizable UI chrome — dialogue boxes, panels, buttons — from a single small source image.

**Intent:** Draws nine-slice scaled sprites for entities with `NineSliceComponent`.

**Use-case:** Use for UI panels, dialogue boxes, and other resizable elements that must scale without distorting corners. Entities are culled against the camera bounds before drawing unless their `TargetSpriteBatch` is the UI batch, which is not camera-relative.

**Implements:** _[IMurderRenderSystem](../../../Murder/Core/Graphics/IMurderRenderSystem.html), [IRenderSystem](../../../Bang/Systems/IRenderSystem.html), [ISystem](../../../Bang/Systems/ISystem.html)_

### ⭐ Constructors

```csharp
public SpriteNineSliceRenderSystem()
```

### ⭐ Methods

#### Draw(RenderContext, Context)

```csharp
public virtual void Draw(RenderContext render, Context context)
```

For each filtered entity, skips it if it falls outside the camera bounds (unless it targets the UI batch), then draws its nine-slice sprite stretched to `NineSliceComponent.Target` using `NineSliceComponent.Style`, sorted by the entity's Y position plus `NineSliceComponent.YSortOffset`.

**Parameters** \
`render` [RenderContext](../../../Murder/Core/Graphics/RenderContext.html) \
`context` [Context](../../../Bang/Contexts/Context.html) \

⚡
