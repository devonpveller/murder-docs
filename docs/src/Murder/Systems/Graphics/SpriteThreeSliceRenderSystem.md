# SpriteThreeSliceRenderSystem

**Namespace:** Murder.Systems.Graphics \
**Assembly:** Murder.dll

```csharp
public class SpriteThreeSliceRenderSystem : IMurderRenderSystem, IRenderSystem, ISystem
```

Draws every visible entity with a [ThreeSliceComponent](../../../Murder/Components/Graphics/ThreeSliceComponent.html) by stretching the sprite's center slice (`CoreSliceRectangle`) along a single axis to reach `Size`, keeping the two end caps undistorted. This is the one-axis counterpart to nine-slicing.

**Intent:** Draws three-slice scaled sprites for entities with `ThreeSliceComponent`.

**Use-case:** Use for health bars, progress bars, and other one-axis-resizable UI or game elements. `ThreeSliceComponent` requires a `SpriteComponent` on the same entity to supply the source frame, and `SpriteRenderSystem` explicitly skips any entity that has a `ThreeSliceComponent` so the two systems never draw the same sprite twice. Only the current animation's evaluated frame is drawn — animated three-slices are not currently supported. It is marked with `[EditorSystem]`, so it also runs inside the level editor's preview stage.

**Implements:** _[IMurderRenderSystem](../../../Murder/Core/Graphics/IMurderRenderSystem.html), [IRenderSystem](../../../Bang/Systems/IRenderSystem.html), [ISystem](../../../Bang/Systems/ISystem.html)_

### ⭐ Constructors

```csharp
public SpriteThreeSliceRenderSystem()
```

### ⭐ Methods

#### Draw(RenderContext, Context)

```csharp
public virtual void Draw(RenderContext render, Context context)
```

For each filtered entity, resolves its `SpriteComponent`'s current animation frame, skips drawing if it is out of the camera bounds (unless targeting the UI batch) or its animation/asset cannot be found, then draws the frame three-sliced according to `CoreSliceRectangle`, `Size`, and `Orientation`.

**Parameters** \
`render` [RenderContext](../../../Murder/Core/Graphics/RenderContext.html) \
`context` [Context](../../../Bang/Contexts/Context.html) \

⚡
