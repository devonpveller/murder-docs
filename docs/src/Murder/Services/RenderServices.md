# RenderServices

**Namespace:** Murder.Services \
**Assembly:** Murder.dll

```csharp
public static partial class RenderServices
```

Core rendering utility class providing methods for drawing sprites, shapes, text, nine-slices, and UI menus into a `Batch2D`.

**Intent:** Centralises essentially all 2D drawing operations — sprites/portraits, primitive shapes (lines, circles, polygons, rectangles), text, nine/three-slice panels, vertical menus, animation-event bookkeeping, and raw texture/vertex submission — so game systems and interactions can render content and react to animation playback without directly managing batches, atlases, or the graphics device.

**Use-case:** Call the `DrawSprite` family to render animated sprites, `DrawText`/`DrawSimpleText` for labels, `Draw9Slice`/`Draw3Slice` for scalable UI panels, `DrawVerticalMenu` for simple interactive menus, and the shape primitives (`DrawLine`, `DrawRectangle`, `DrawCircleOutline`, etc.) for debug or gameplay overlays. Call `TriggerEventsIfNeeded`/`MessageCompleteAnimations` from animation-driving systems to fire animation frame/complete events at the right time.

### ⭐ Properties

#### BLEND_COLOR_ONLY

```csharp
public static Vector3 BLEND_COLOR_ONLY = new(0, 0, 1);
```

Blend vector that applies only the color channel while discarding the original sprite colors (tint-only mode). Used by `DrawRectangle`/`DrawQuad` so solid-color shapes ignore any texture data.

**Returns** \
[Vector3](https://docs.monogame.net/api/Microsoft.Xna.Framework.Vector3.html) \

#### BLEND_NORMAL

```csharp
public static Vector3 BLEND_NORMAL = new(1, 0, 0);
```

Default blend vector that draws the sprite with its original colors unchanged.

**Returns** \
[Vector3](https://docs.monogame.net/api/Microsoft.Xna.Framework.Vector3.html) \

#### BLEND_WASH

```csharp
public static Vector3 BLEND_WASH = new(0, 1, 0);
```

Blend vector that washes the sprite toward the tint color, mixing original and tint hues. Used internally to draw outlines/shadows as a solid-colored silhouette of the sprite.

**Returns** \
[Vector3](https://docs.monogame.net/api/Microsoft.Xna.Framework.Vector3.html) \

### ⭐ Methods

#### CanPlayAnimationId(Entity, string)

```csharp
public static bool CanPlayAnimationId(Entity e, string animationId)
```

Returns whether `e`'s current sprite asset actually contains an animation named `animationId`. Use to validate an animation name before attempting to play it (e.g. from data-driven or scripted animation triggers) and avoid a failed/log-spamming `DrawSprite` call.

**Parameters** \
`e` [Entity](../../Bang/Entities/Entity.html) \
`animationId` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### CheckForEvents(RenderedSpriteCache?, Guid, AnimationInfo, FrameInfo)

```csharp
public static string? CheckForEvents(RenderedSpriteCache? previous, Guid currentAnimationGuid, AnimationInfo animationInfo, FrameInfo frameInfo)
```

Non-mutating variant of `TriggerEventsIfNeeded`: given the *previous* rendered-sprite cache snapshot, walks the frames crossed since then and returns the name of the first animation event encountered (or `null` if none), without sending any message itself. Used where the caller wants to inspect/react to the upcoming event name before deciding whether to dispatch it.

**Parameters** \
`previous` [RenderedSpriteCache?](../../Murder/Components/Graphics/RenderedSpriteCache.html) \
`currentAnimationGuid` [Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \
`animationInfo` [AnimationInfo](../../Murder/Core/Graphics/AnimationInfo.html) \
`frameInfo` [FrameInfo](../../Murder/Core/FrameInfo.html) \

**Returns** \
[string?](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### CompleteAnimationOverload(Entity, AnimationOverloadComponent, FrameInfo?, AnimationSpeedOverload?)

```csharp
public static void CompleteAnimationOverload(Entity e, AnimationOverloadComponent overload, FrameInfo? frameInfo, AnimationSpeedOverload? speedOverload)
```

Advances or clears a temporary "animation overload" (a one-off animation played on top of an entity's normal state, e.g. an attack or hit reaction): plays the next queued overload animation if there is one, chains into the overload's configured next animation, or removes the overload and fires the appropriate complete message when it's finished. Also clears a persisted `AnimationSpeedOverload` once the overload animation ends. Called by the sprite-rendering systems once an overload animation finishes playing; not typically invoked directly by gameplay code.

**Parameters** \
`e` [Entity](../../Bang/Entities/Entity.html) \
`overload` [AnimationOverloadComponent](../../Murder/Components/AnimationOverloadComponent.html) \
`frameInfo` [FrameInfo?](../../Murder/Core/FrameInfo.html) \
`speedOverload` [AnimationSpeedOverload?](../../Murder/Components/AnimationSpeedOverload.html) \

#### CreateGameplayScreenshot()

```csharp
public static Texture2D? CreateGameplayScreenshot()
```

Captures the current gameplay render target (`RenderContext.MainTarget`) into a new `Texture2D`, or `null` if there is no active scene/render target. Must only be called on the main thread, since it needs the graphics device; the caller is responsible for disposing the returned texture. Used for things like a pause-menu background blur or a "you died" freeze-frame that should show gameplay without UI.

**Returns** \
[Texture2D?](https://docs.monogame.net/api/Microsoft.Xna.Framework.Graphics.Texture2D.html) \

#### CreateScreenshot()

```csharp
public static Texture2D? CreateScreenshot()
```

Captures the last fully-composited frame (`RenderContext.LastRenderTarget`, i.e. including UI) into a new `Texture2D`, or `null` if there is no active render target. The caller is responsible for disposing the returned texture. Use this (instead of `CreateGameplayScreenshot`) when you want a screenshot of exactly what the player saw, UI included — e.g. for a save-file thumbnail or a share/export feature.

**Returns** \
[Texture2D?](https://docs.monogame.net/api/Microsoft.Xna.Framework.Graphics.Texture2D.html) \

#### CreateScreenshotFromTarget(RenderTarget2D)

```csharp
public static Texture2D? CreateScreenshotFromTarget(RenderTarget2D mainTarget)
```

Copies `mainTarget` into a brand-new `RenderTarget2D` of the same format/size via a texture-quad blit, so the result is safe to keep and use independently of the source target's lifetime (which may get reused/cleared by the renderer next frame). Underlies both `CreateGameplayScreenshot` and `CreateScreenshot`; must only be called on the main thread, and the caller must dispose the result.

**Parameters** \
`mainTarget` [RenderTarget2D](https://docs.monogame.net/api/Microsoft.Xna.Framework.Graphics.RenderTarget2D.html) \

**Returns** \
[Texture2D?](https://docs.monogame.net/api/Microsoft.Xna.Framework.Graphics.Texture2D.html) \

#### CurrentTime(AnimationInfo)

```csharp
public static float CurrentTime(this AnimationInfo @this)
```

Returns the time to use when evaluating `@this`'s current animation frame: `OverrideCurrentTime` if it was explicitly set (not `-1`), otherwise `Game.Now` or `Game.NowUnscaled` depending on `UseScaledTime`. Used internally by the `DrawSprite` overloads that take an `AnimationInfo`, and useful directly when a caller needs to know "what time is this animation effectively at right now" (e.g. to sync a sound effect to a specific frame).

**Parameters** \
`this` [AnimationInfo](../../Murder/Core/Graphics/AnimationInfo.html) \

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### Draw3Slice(Batch2D, AtlasCoordinates, Rectangle, Vector2, Vector2, Vector2, Orientation, float)

```csharp
public static void Draw3Slice(Batch2D batch, AtlasCoordinates texture, Rectangle core, Vector2 position, Vector2 size, Vector2 origin, Orientation orientation, float sort)
```

Draws a three-slice (horizontal or vertical) stretched texture between `position` and `size`, keeping the two end caps (defined by `core`) unstretched while the middle segment stretches to fill the remaining length. Used for elongated UI elements that should stretch along one axis only (e.g. a progress bar or a scroll track), as opposed to `Draw9Slice`'s two-axis stretching.

**Parameters** \
`batch` [Batch2D](../../Murder/Core/Graphics/Batch2D.html) \
`texture` [AtlasCoordinates](../../Murder/Core/Graphics/AtlasCoordinates.html) \
`core` [Rectangle](../../Murder/Core/Geometry/Rectangle.html) \
`position` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`size` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`origin` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`orientation` [Orientation](../../Murder/Core/Orientation.html) \
`sort` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### Draw9Slice(Batch2D, AtlasCoordinates, IntRectangle, IntRectangle, NineSliceStyle, DrawInfo)

```csharp
public static void Draw9Slice(Batch2D batch, AtlasCoordinates texture, IntRectangle core, IntRectangle target, NineSliceStyle style, DrawInfo info)
```

The core nine-slice implementation: draws `texture` stretched (or tiled, depending on `style`) to fill `target`, keeping the four corners defined by `core` unstretched, and drawing outline/shadow passes first if `info` requests them. Every other `Draw9Slice`/`Draw9SliceWithText` overload eventually calls this one; call it directly when you already have raw atlas coordinates rather than a sprite asset guid.

**Parameters** \
`batch` [Batch2D](../../Murder/Core/Graphics/Batch2D.html) \
`texture` [AtlasCoordinates](../../Murder/Core/Graphics/AtlasCoordinates.html) \
`core` [IntRectangle](../../Murder/Core/Geometry/IntRectangle.html) \
`target` [IntRectangle](../../Murder/Core/Geometry/IntRectangle.html) \
`style` [NineSliceStyle](../../Murder/Core/Graphics/NineSliceStyle.html) \
`info` [DrawInfo](../../Murder/Core/Graphics/DrawInfo.html) \

#### Draw9Slice(Batch2D, Guid, Rectangle, DrawInfo)

```csharp
public static void Draw9Slice(Batch2D batch, Guid guid, Rectangle target, DrawInfo drawInfo)
```

Draws the sprite asset `guid`'s current frame as a nine-slice stretched to fill `target`, using the sprite's default animation and `NineSliceStyle.Stretch`. The core rectangle used for the slicing comes from the sprite asset's Aseprite-authored nine-slice data.

**Parameters** \
`batch` [Batch2D](../../Murder/Core/Graphics/Batch2D.html) \
`guid` [Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \
`target` [Rectangle](../../Murder/Core/Geometry/Rectangle.html) \
`drawInfo` [DrawInfo](../../Murder/Core/Graphics/DrawInfo.html) \

#### Draw9Slice(Batch2D, Guid, Rectangle, DrawInfo, AnimationInfo)

```csharp
public static void Draw9Slice(Batch2D batch, Guid guid, Rectangle target, DrawInfo drawInfo, AnimationInfo animationInfo)
```

Same as `Draw9Slice(Batch2D, Guid, Rectangle, DrawInfo)`, but evaluates `animationInfo` to pick which animated frame of the sprite asset to nine-slice (with `NineSliceStyle.Stretch`), instead of always the default animation.

**Parameters** \
`batch` [Batch2D](../../Murder/Core/Graphics/Batch2D.html) \
`guid` [Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \
`target` [Rectangle](../../Murder/Core/Geometry/Rectangle.html) \
`drawInfo` [DrawInfo](../../Murder/Core/Graphics/DrawInfo.html) \
`animationInfo` [AnimationInfo](../../Murder/Core/Graphics/AnimationInfo.html) \

#### Draw9Slice(Batch2D, Guid, Rectangle, NineSliceStyle, DrawInfo, AnimationInfo)

```csharp
public static void Draw9Slice(Batch2D batch, Guid guid, Rectangle target, NineSliceStyle style, DrawInfo drawInfo, AnimationInfo animationInfo)
```

Full-control overload of `Draw9Slice` for a sprite asset: picks the animated frame via `animationInfo` and draws it with the given `style` (stretch vs. tile, and whether the center is hollow). Logs and no-ops if `animationInfo.Name` isn't a valid animation on the asset.

**Parameters** \
`batch` [Batch2D](../../Murder/Core/Graphics/Batch2D.html) \
`guid` [Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \
`target` [Rectangle](../../Murder/Core/Geometry/Rectangle.html) \
`style` [NineSliceStyle](../../Murder/Core/Graphics/NineSliceStyle.html) \
`drawInfo` [DrawInfo](../../Murder/Core/Graphics/DrawInfo.html) \
`animationInfo` [AnimationInfo](../../Murder/Core/Graphics/AnimationInfo.html) \

#### Draw9SliceWithText(Batch2D, Guid, string, int, Rectangle, DrawInfo, DrawInfo, AnimationInfo, int, int)

```csharp
public static Point Draw9SliceWithText(Batch2D batch, Guid sprite, string text, int font, Rectangle target, DrawInfo textDrawInfo, DrawInfo sliceDrawInfo, AnimationInfo sliceAnimationInfo, int padding, int textPadding)
```

Draws `text` word-wrapped to `target`'s width, resizes `target`'s height to fit the wrapped text plus `padding`, then draws a nine-slice `sprite` behind it (offset by `textPadding`), and returns the final `(width, height)` used. This is the primitive behind auto-sizing dialogue/tooltip boxes: give it the box width and text, and it grows the box to fit rather than requiring the caller to pre-measure the text.

**Parameters** \
`batch` [Batch2D](../../Murder/Core/Graphics/Batch2D.html) \
`sprite` [Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \
`text` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
`font` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`target` [Rectangle](../../Murder/Core/Geometry/Rectangle.html) \
`textDrawInfo` [DrawInfo](../../Murder/Core/Graphics/DrawInfo.html) \
`sliceDrawInfo` [DrawInfo](../../Murder/Core/Graphics/DrawInfo.html) \
`sliceAnimationInfo` [AnimationInfo](../../Murder/Core/Graphics/AnimationInfo.html) \
`padding` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`textPadding` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

**Returns** \
[Point](../../Murder/Core/Geometry/Point.html) \

#### DealWithCompleteAnimations(Entity, SpriteComponent)

```csharp
public static void DealWithCompleteAnimations(Entity e, SpriteComponent s)
```

Advances `e`'s sprite to the next queued animation in `s.NextAnimations` if there is one, otherwise marks the current animation as complete and sends the appropriate complete message. Called by the sprite-rendering systems each time a non-overload animation finishes.

**Parameters** \
`e` [Entity](../../Bang/Entities/Entity.html) \
`s` [SpriteComponent](../../Murder/Components/SpriteComponent.html) \

#### DrawArrow(Batch2D, Vector2, Vector2, Color, float, float, float)

```csharp
public static void DrawArrow(this Batch2D spriteBatch, Vector2 point1, Vector2 point2, Color color, float thickness, float headSize, float sort = 1f)
```

Draws a line from `point1` to `point2` with a filled arrowhead of size `headSize` at `point2`. Useful for debug-drawing directions, forces, or paths.

**Parameters** \
`spriteBatch` [Batch2D](../../Murder/Core/Graphics/Batch2D.html) \
`point1` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`point2` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`color` [Color](../../Murder/Core/Graphics/Color.html) \
`thickness` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`headSize` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`sort` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### DrawCircleOutline(Batch2D, Point, float, int, Color, float)

```csharp
public static void DrawCircleOutline(this Batch2D spriteBatch, Point center, float radius, int sides, Color color, float sort = 1f)
```

Draws a wireframe circle centred at integer point `center`, approximated with `sides` line segments.

**Parameters** \
`spriteBatch` [Batch2D](../../Murder/Core/Graphics/Batch2D.html) \
`center` [Point](../../Murder/Core/Geometry/Point.html) \
`radius` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`sides` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`color` [Color](../../Murder/Core/Graphics/Color.html) \
`sort` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### DrawCircleOutline(Batch2D, Rectangle, int, Color)

```csharp
public static void DrawCircleOutline(this Batch2D spriteBatch, Rectangle rectangle, int sides, Color color)
```

Draws a wireframe ellipse inscribed within `rectangle` (the rectangle's width/height are used as the ellipse's scale).

**Parameters** \
`spriteBatch` [Batch2D](../../Murder/Core/Graphics/Batch2D.html) \
`rectangle` [Rectangle](../../Murder/Core/Geometry/Rectangle.html) \
`sides` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`color` [Color](../../Murder/Core/Graphics/Color.html) \

#### DrawCircleOutline(Batch2D, Vector2, float, int, Color, float)

```csharp
public static void DrawCircleOutline(this Batch2D spriteBatch, Vector2 center, float radius, int sides, Color color, float sort = 1f)
```

Draws a wireframe circle centred at `center`, approximated with `sides` line segments. The float-position overload other `DrawCircleOutline` overloads delegate to.

**Parameters** \
`spriteBatch` [Batch2D](../../Murder/Core/Graphics/Batch2D.html) \
`center` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`radius` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`sides` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`color` [Color](../../Murder/Core/Graphics/Color.html) \
`sort` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### DrawCircleSector(Batch2D, Vector2, float, float, float, int, DrawInfo?)

```csharp
public static void DrawCircleSector(this Batch2D batch, Vector2 center, float radius, float startAngle, float endAngle, int steps, DrawInfo? drawInfo = default)
```

Draws a filled "pie slice" of a circle centred at `center`, spanning from `startAngle` to `endAngle` (radians). If the angular span covers a full circle it falls back to `DrawFilledCircle`. Used for radial UI elements such as cooldown/charge indicators.

**Parameters** \
`batch` [Batch2D](../../Murder/Core/Graphics/Batch2D.html) \
`center` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`radius` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`startAngle` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`endAngle` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`steps` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`drawInfo` [DrawInfo?](../../Murder/Core/Graphics/DrawInfo.html) \

#### DrawFilledCircle(Batch2D, Rectangle, int, DrawInfo)

```csharp
public static void DrawFilledCircle(this Batch2D batch, Rectangle circleRect, int steps, DrawInfo drawInfo)
```

Draws a filled circle (approximated as a `steps`-sided polygon) inscribed within `circleRect`.

**Parameters** \
`batch` [Batch2D](../../Murder/Core/Graphics/Batch2D.html) \
`circleRect` [Rectangle](../../Murder/Core/Geometry/Rectangle.html) \
`steps` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`drawInfo` [DrawInfo](../../Murder/Core/Graphics/DrawInfo.html) \

#### DrawFilledCircle(Batch2D, Vector2, float, int, DrawInfo?)

```csharp
public static void DrawFilledCircle(this Batch2D batch, Vector2 center, float radius, int steps, DrawInfo? drawInfo = default)
```

Draws a filled circle (approximated as a `steps`-sided polygon) centred at `center` with the given `radius`, without allocating per call.

**Parameters** \
`batch` [Batch2D](../../Murder/Core/Graphics/Batch2D.html) \
`center` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`radius` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`steps` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`drawInfo` [DrawInfo?](../../Murder/Core/Graphics/DrawInfo.html) \

#### DrawHorizontalLine(Batch2D, int, int, int, Color, float)

```csharp
public static void DrawHorizontalLine(this Batch2D spriteBatch, int x, int y, int length, Color color, float sorting = 0)
```

Draws a single-pixel-tall horizontal line of `length` pixels starting at `(x, y)`.

**Parameters** \
`spriteBatch` [Batch2D](../../Murder/Core/Graphics/Batch2D.html) \
`x` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`y` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`length` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`color` [Color](../../Murder/Core/Graphics/Color.html) \
`sorting` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### DrawIndexedVertices&lt;T&gt;(GraphicsDevice, T[], int, short[], int, Effect, BlendState, Texture2D, bool)

```csharp
public static void DrawIndexedVertices<T>(GraphicsDevice graphicsDevice, T[] vertices, int vertexCount, short[] indices, int primitiveCount, Effect? effect, BlendState? blendState = null, Texture2D? texture = null, bool smoothing = false) where T : struct, IVertexType
```

Submits raw indexed vertex/triangle data directly to the graphics device using `effect` (applying every pass), bypassing `Batch2D` entirely. This is the low-level primitive that `DrawTextureQuad`/`DrawQuad`/`DrawQuadOutline` are built on; reach for it directly only when implementing new custom-mesh rendering that doesn't fit the sprite-batch model.

**Parameters** \
`graphicsDevice` [GraphicsDevice](https://docs.monogame.net/api/Microsoft.Xna.Framework.Graphics.GraphicsDevice.html) \
`vertices` `T[]` \
`vertexCount` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`indices` [short[]](https://learn.microsoft.com/en-us/dotnet/api/System.Int16?view=net-7.0) \
`primitiveCount` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`effect` [Effect](https://docs.monogame.net/api/Microsoft.Xna.Framework.Graphics.Effect.html) \
`blendState` [BlendState](https://docs.monogame.net/api/Microsoft.Xna.Framework.Graphics.BlendState.html) \
`texture` [Texture2D](https://docs.monogame.net/api/Microsoft.Xna.Framework.Graphics.Texture2D.html) \
`smoothing` [bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### DrawLine(Batch2D, Point, Point, Color, float)

```csharp
public static void DrawLine(this Batch2D spriteBatch, Point point1, Point point2, Color color, float sort = 1f)
```

Draws a 1px-thick line segment between two integer-coordinate points.

**Parameters** \
`spriteBatch` [Batch2D](../../Murder/Core/Graphics/Batch2D.html) \
`point1` [Point](../../Murder/Core/Geometry/Point.html) \
`point2` [Point](../../Murder/Core/Geometry/Point.html) \
`color` [Color](../../Murder/Core/Graphics/Color.html) \
`sort` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### DrawLine(Batch2D, Vector2, float, float, Color, float)

```csharp
public static void DrawLine(this Batch2D spriteBatch, Vector2 point, float length, float angle, Color color, float sort = 1f)
```

Draws a 1px-thick line of `length` pixels starting at `point` and extending in the direction of `angle` (radians). The other `DrawLine`/`DrawArrow` overloads eventually reduce to this angle-based draw call.

**Parameters** \
`spriteBatch` [Batch2D](../../Murder/Core/Graphics/Batch2D.html) \
`point` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`length` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`angle` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`color` [Color](../../Murder/Core/Graphics/Color.html) \
`sort` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### DrawLine(Batch2D, Vector2, float, float, Color, float, float)

```csharp
public static void DrawLine(this Batch2D spriteBatch, Vector2 point, float length, float angle, Color color, float thickness, float sort = 1f)
```

Draws a line of `length` pixels at `angle` (radians) with a custom `thickness`, extending an extra `0.75` pixels beyond `length` to avoid a 1px visual gap at line joints.

**Parameters** \
`spriteBatch` [Batch2D](../../Murder/Core/Graphics/Batch2D.html) \
`point` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`length` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`angle` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`color` [Color](../../Murder/Core/Graphics/Color.html) \
`thickness` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`sort` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### DrawLine(Batch2D, Vector2, Vector2, Color, float)

```csharp
public static void DrawLine(this Batch2D spriteBatch, Vector2 point1, Vector2 point2, Color color, float sort = 1f)
```

Draws a 1px-thick line segment between two float-precision world positions.

**Parameters** \
`spriteBatch` [Batch2D](../../Murder/Core/Graphics/Batch2D.html) \
`point1` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`point2` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`color` [Color](../../Murder/Core/Graphics/Color.html) \
`sort` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### DrawLine(Batch2D, Vector2, Vector2, Color, float, float)

```csharp
public static void DrawLine(this Batch2D spriteBatch, Vector2 point1, Vector2 point2, Color color, float thickness, float sort = 1f)
```

Draws a line segment between two float-precision positions with a custom `thickness`, computing the distance/angle between them and delegating to the angle-based `DrawLine` overload.

**Parameters** \
`spriteBatch` [Batch2D](../../Murder/Core/Graphics/Batch2D.html) \
`point1` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`point2` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`color` [Color](../../Murder/Core/Graphics/Color.html) \
`thickness` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`sort` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### DrawLineShort(Batch2D, Vector2, float, float, Color, float, float)

```csharp
public static void DrawLineShort(this Batch2D spriteBatch, Vector2 point, float length, float angle, Color color, float thickness, float sort = 1f)
```

Same as the angle-based `DrawLine` overload, but without the `0.75`-pixel length pad — the line stops exactly at `length`. Used where an exact endpoint matters (e.g. `DrawArrow`'s shaft, so the arrowhead isn't overlapped).

**Parameters** \
`spriteBatch` [Batch2D](../../Murder/Core/Graphics/Batch2D.html) \
`point` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`length` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`angle` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`color` [Color](../../Murder/Core/Graphics/Color.html) \
`thickness` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`sort` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### DrawLineShort(Batch2D, Vector2, Vector2, Color, float, float)

```csharp
public static void DrawLineShort(this Batch2D spriteBatch, Vector2 point1, Vector2 point2, Color color, float thickness, float sort = 1f)
```

Point-to-point overload of `DrawLineShort`, computing distance/angle between `point1` and `point2` and delegating to the angle-based overload.

**Parameters** \
`spriteBatch` [Batch2D](../../Murder/Core/Graphics/Batch2D.html) \
`point1` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`point2` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`color` [Color](../../Murder/Core/Graphics/Color.html) \
`thickness` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`sort` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### DrawPartialCircleOutline(Batch2D, Point, float, int, int, int, float, Color, float, bool)

```csharp
public static void DrawPartialCircleOutline(this Batch2D spriteBatch, Point center, float radius, int sides, int start, int end, float thickness, Color color, float sort = 1f, bool closeShape = true)
```

Draws only a subset (from vertex index `start` to `end`) of a `sides`-sided circle outline, optionally closing the arc back to its start point. Use for partial-ring UI elements like a segmented cooldown indicator, as opposed to `DrawCircleOutline`'s always-full circle.

**Parameters** \
`spriteBatch` [Batch2D](../../Murder/Core/Graphics/Batch2D.html) \
`center` [Point](../../Murder/Core/Geometry/Point.html) \
`radius` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`sides` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`start` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`end` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`thickness` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`color` [Color](../../Murder/Core/Graphics/Color.html) \
`sort` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`closeShape` [bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### DrawPoint(Batch2D, Point, Color, float)

```csharp
public static void DrawPoint(this Batch2D spriteBatch, Point pos, Color color, float sorting = 0)
```

Draws a single 1x1-pixel point at `pos`.

**Parameters** \
`spriteBatch` [Batch2D](../../Murder/Core/Graphics/Batch2D.html) \
`pos` [Point](../../Murder/Core/Geometry/Point.html) \
`color` [Color](../../Murder/Core/Graphics/Color.html) \
`sorting` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### DrawPoints(Batch2D, Vector2, Vector2, ImmutableArray&lt;Vector2&gt;, Color, float, float)

```csharp
public static void DrawPoints(this Batch2D spriteBatch, Vector2 position, Vector2 scale, ImmutableArray<Vector2> points, Color color, float thickness, float sort)
```

Draws a closed loop connecting every point in `points` (scaled by `scale` and offset by `position`) with straight line segments — the last point always connects back to the first. Used to outline arbitrary polygons (e.g. `DrawCircleOutline` draws its unit-circle points this way).

**Parameters** \
`spriteBatch` [Batch2D](../../Murder/Core/Graphics/Batch2D.html) \
`position` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`scale` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`points` [ImmutableArray\<Vector2\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \
`color` [Color](../../Murder/Core/Graphics/Color.html) \
`thickness` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`sort` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### DrawPoints(Batch2D, Vector2, Vector2, ImmutableArray&lt;Vector2&gt;, Color, float)

```csharp
public static void DrawPoints(this Batch2D spriteBatch, Vector2 position, Vector2 scale, ImmutableArray<Vector2> points, Color color, float thickness)
```

Same as the sort-taking overload, using the default sort depth.

**Parameters** \
`spriteBatch` [Batch2D](../../Murder/Core/Graphics/Batch2D.html) \
`position` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`scale` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`points` [ImmutableArray\<Vector2\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \
`color` [Color](../../Murder/Core/Graphics/Color.html) \
`thickness` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### DrawPoints(Batch2D, Vector2, Vector2, ReadOnlySpan&lt;Vector2&gt;, Color, float, float, bool)

```csharp
public static void DrawPoints(this Batch2D spriteBatch, Vector2 position, Vector2 scale, ReadOnlySpan<Vector2> points, Color color, float thickness, float sort, bool closeShape)
```

Zero-allocation span overload of `DrawPoints`, with an explicit `closeShape` flag so the caller can draw an open polyline instead of always closing the loop back to the first point. Used by `DrawPartialCircleOutline` to draw arcs that shouldn't necessarily close.

**Parameters** \
`spriteBatch` [Batch2D](../../Murder/Core/Graphics/Batch2D.html) \
`position` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`scale` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`points` [ReadOnlySpan\<Vector2\>](https://learn.microsoft.com/en-us/dotnet/api/System.ReadOnlySpan-1?view=net-7.0) \
`color` [Color](../../Murder/Core/Graphics/Color.html) \
`thickness` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`sort` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`closeShape` [bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### DrawPolygon(Batch2D, Vector2, ImmutableArray&lt;Vector2&gt;, DrawInfo?)

```csharp
public static void DrawPolygon(this Batch2D batch, Vector2 position, ImmutableArray<Vector2> vertices, DrawInfo? drawInfo = default)
```

Draws a filled, closed polygon from `vertices` (relative to `position`) as a single textured pixel-quad batch draw, using a shared 1x1 pixel texture as the fill.

**Parameters** \
`batch` [Batch2D](../../Murder/Core/Graphics/Batch2D.html) \
`position` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`vertices` [ImmutableArray\<Vector2\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \
`drawInfo` [DrawInfo?](../../Murder/Core/Graphics/DrawInfo.html) \

#### DrawPortrait(Batch2D, Portrait, Vector2, DrawInfo)

```csharp
public static FrameInfo DrawPortrait(this Batch2D batch, Portrait portrait, Vector2 position, DrawInfo drawInfo)
```

Resolves `portrait` to its sprite asset/animation (via `FetchPortraitAsSprite`) and draws it at `position`, or returns `FrameInfo.Fail` if the portrait's sprite asset can't be found. Convenience wrapper for drawing character portraits (dialogue boxes, character select, etc.) without manually resolving the underlying sprite asset.

**Parameters** \
`batch` [Batch2D](../../Murder/Core/Graphics/Batch2D.html) \
`portrait` [Portrait](../../Murder/Core/Portrait.html) \
`position` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`drawInfo` [DrawInfo](../../Murder/Core/Graphics/DrawInfo.html) \

**Returns** \
[FrameInfo](../../Murder/Core/FrameInfo.html) \

#### DrawQuad(Rectangle, Color)

```csharp
public static void DrawQuad(Rectangle rect, Color color)
```

Fills `rect` with `color` using a direct indexed-vertex draw (bypassing `Batch2D`'s sort/atlas machinery), useful for full-screen or full-viewport overlays that don't need sprite-batch sorting.

**Parameters** \
`rect` [Rectangle](../../Murder/Core/Geometry/Rectangle.html) \
`color` [Color](../../Murder/Core/Graphics/Color.html) \

#### DrawQuadOutline(Rectangle, Color)

```csharp
public static void DrawQuadOutline(Rectangle rect, Color color)
```

Draws a single-pixel border around `rect` using four `DrawQuad` calls, one per edge.

**Parameters** \
`rect` [Rectangle](../../Murder/Core/Geometry/Rectangle.html) \
`color` [Color](../../Murder/Core/Graphics/Color.html) \

#### DrawRectangle(Batch2D, Rectangle, Color, float)

```csharp
public static void DrawRectangle(this Batch2D batch, Rectangle rectangle, Color color, float sorting = 0)
```

Fills `rectangle` with a solid `color` at the given sort depth, using `BLEND_COLOR_ONLY` so the shared pixel texture's own color is ignored.

**Parameters** \
`batch` [Batch2D](../../Murder/Core/Graphics/Batch2D.html) \
`rectangle` [Rectangle](../../Murder/Core/Geometry/Rectangle.html) \
`color` [Color](../../Murder/Core/Graphics/Color.html) \
`sorting` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### DrawRectangle(Batch2D, Rectangle, DrawInfo)

```csharp
public static void DrawRectangle(this Batch2D batch, Rectangle rectangle, DrawInfo drawInfo)
```

Fills `rectangle` using the full `DrawInfo` (color, rotation, blend state, sort) instead of just a flat color, for cases that need rotation or a custom blend mode on a filled rectangle.

**Parameters** \
`batch` [Batch2D](../../Murder/Core/Graphics/Batch2D.html) \
`rectangle` [Rectangle](../../Murder/Core/Geometry/Rectangle.html) \
`drawInfo` [DrawInfo](../../Murder/Core/Graphics/DrawInfo.html) \

#### DrawRectangleOutline(Batch2D, Rectangle, Color)

```csharp
public static void DrawRectangleOutline(this Batch2D spriteBatch, Rectangle rectangle, Color color)
```

Draws a single-pixel border around `rectangle`.

**Parameters** \
`spriteBatch` [Batch2D](../../Murder/Core/Graphics/Batch2D.html) \
`rectangle` [Rectangle](../../Murder/Core/Geometry/Rectangle.html) \
`color` [Color](../../Murder/Core/Graphics/Color.html) \

#### DrawRectangleOutline(Batch2D, Rectangle, Color, int)

```csharp
public static void DrawRectangleOutline(this Batch2D spriteBatch, Rectangle rectangle, Color color, int lineWidth)
```

Draws the border of `rectangle` with `lineWidth`-pixel thickness.

**Parameters** \
`spriteBatch` [Batch2D](../../Murder/Core/Graphics/Batch2D.html) \
`rectangle` [Rectangle](../../Murder/Core/Geometry/Rectangle.html) \
`color` [Color](../../Murder/Core/Graphics/Color.html) \
`lineWidth` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### DrawRectangleOutline(Batch2D, Rectangle, Color, int, float)

```csharp
public static void DrawRectangleOutline(this Batch2D spriteBatch, Rectangle rectangle, Color color, int lineWidth, float sorting)
```

Draws the border of `rectangle` with `lineWidth`-pixel thickness at `sorting` depth, using four filled `DrawRectangle` calls (one per edge, drawn slightly inset so they meet cleanly at corners).

**Parameters** \
`spriteBatch` [Batch2D](../../Murder/Core/Graphics/Batch2D.html) \
`rectangle` [Rectangle](../../Murder/Core/Geometry/Rectangle.html) \
`color` [Color](../../Murder/Core/Graphics/Color.html) \
`lineWidth` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`sorting` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### DrawRepeating(Batch2D, AtlasCoordinates, Rectangle, float)

```csharp
public static void DrawRepeating(Batch2D batch, AtlasCoordinates texture, Rectangle area, float sort)
```

Tiles `texture` repeatedly to fill `area`, clipping the edge tiles so the pattern doesn't overflow the rectangle's bounds. Used for scrolling/repeating backgrounds and textured panel fills.

**Parameters** \
`batch` [Batch2D](../../Murder/Core/Graphics/Batch2D.html) \
`texture` [AtlasCoordinates](../../Murder/Core/Graphics/AtlasCoordinates.html) \
`area` [Rectangle](../../Murder/Core/Geometry/Rectangle.html) \
`sort` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### DrawSimpleText(Batch2D, int, string, Vector2, DrawInfo)

```csharp
public static Point DrawSimpleText(this Batch2D uiBatch, int pixelFont, string text, Vector2 position, DrawInfo drawInfo)
```

Draws `text` without line wrapping, inline color formatting (`<c=...>` tags), or any of the other rich-text features `DrawText` supports — a cheaper path for short, plain labels where that overhead isn't needed. Returns the drawn text's pixel size.

**Parameters** \
`uiBatch` [Batch2D](../../Murder/Core/Graphics/Batch2D.html) \
`pixelFont` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`text` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
`position` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`drawInfo` [DrawInfo](../../Murder/Core/Graphics/DrawInfo.html) \

**Returns** \
[Point](../../Murder/Core/Geometry/Point.html) \

#### DrawSprite(Batch2D, Guid, float, float, DrawInfo, AnimationInfo)

```csharp
public static FrameInfo DrawSprite(this Batch2D batch, Guid assetGuid, float x, float y, DrawInfo drawInfo, AnimationInfo animationInfo)
```

Draws the sprite asset identified by `assetGuid` at pixel coordinates `(x, y)`. Convenience overload of the `Vector2`-position `DrawSprite(Guid, ...)` overload for callers that already have separate x/y floats.

**Parameters** \
`batch` [Batch2D](../../Murder/Core/Graphics/Batch2D.html) \
`assetGuid` [Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \
`x` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`y` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`drawInfo` [DrawInfo](../../Murder/Core/Graphics/DrawInfo.html) \
`animationInfo` [AnimationInfo](../../Murder/Core/Graphics/AnimationInfo.html) \

**Returns** \
[FrameInfo](../../Murder/Core/FrameInfo.html) \

#### DrawSprite(Batch2D, Guid, Vector2, DrawInfo?)

```csharp
public static FrameInfo DrawSprite(this Batch2D batch, Guid assetGuid, Vector2 position, DrawInfo? drawInfo = default)
```

Draws the sprite asset identified by `assetGuid` at `position` with its default animation, using default draw parameters if `drawInfo` is omitted. The most convenient overload when you only have a sprite asset guid and a position.

**Parameters** \
`batch` [Batch2D](../../Murder/Core/Graphics/Batch2D.html) \
`assetGuid` [Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \
`position` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`drawInfo` [DrawInfo?](../../Murder/Core/Graphics/DrawInfo.html) \

**Returns** \
[FrameInfo](../../Murder/Core/FrameInfo.html) \

#### DrawSprite(Batch2D, Guid, Vector2, DrawInfo, AnimationInfo)

```csharp
public static FrameInfo DrawSprite(this Batch2D batch, Guid assetGuid, Vector2 position, DrawInfo drawInfo, AnimationInfo animationInfo)
```

Resolves `assetGuid` to a `SpriteAsset` (returning `FrameInfo.Fail` if not found) and draws it at `position` with an explicit `animationInfo`, rather than the asset's default animation.

**Parameters** \
`batch` [Batch2D](../../Murder/Core/Graphics/Batch2D.html) \
`assetGuid` [Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \
`position` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`drawInfo` [DrawInfo](../../Murder/Core/Graphics/DrawInfo.html) \
`animationInfo` [AnimationInfo](../../Murder/Core/Graphics/AnimationInfo.html) \

**Returns** \
[FrameInfo](../../Murder/Core/FrameInfo.html) \

#### DrawSprite(Batch2D, SpriteAsset, Vector2, DrawInfo?)

```csharp
public static FrameInfo DrawSprite(this Batch2D batch, SpriteAsset asset, Vector2 position, DrawInfo? drawInfo = default)
```

Draws `asset` at `position` with its default animation, using default draw parameters if `drawInfo` is omitted.

**Parameters** \
`batch` [Batch2D](../../Murder/Core/Graphics/Batch2D.html) \
`asset` [SpriteAsset](../../Murder/Assets/Graphics/SpriteAsset.html) \
`position` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`drawInfo` [DrawInfo?](../../Murder/Core/Graphics/DrawInfo.html) \

**Returns** \
[FrameInfo](../../Murder/Core/FrameInfo.html) \

#### DrawSprite(Batch2D, SpriteAsset, Vector2, DrawInfo, AnimationInfo)

```csharp
public static FrameInfo DrawSprite(this Batch2D batch, SpriteAsset asset, Vector2 position, DrawInfo drawInfo, AnimationInfo animationInfo)
```

The core sprite-drawing routine most other `DrawSprite` overloads eventually call: evaluates `animationInfo` against `asset`'s animations to find the current frame, then draws it (plus outline/shadow passes as configured by `drawInfo`) at `position`. Draws a magenta-flashing debug placeholder in `DEBUG` builds if the frame evaluation failed (e.g. unknown animation name).

**Parameters** \
`batch` [Batch2D](../../Murder/Core/Graphics/Batch2D.html) \
`asset` [SpriteAsset](../../Murder/Assets/Graphics/SpriteAsset.html) \
`position` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`drawInfo` [DrawInfo](../../Murder/Core/Graphics/DrawInfo.html) \
`animationInfo` [AnimationInfo](../../Murder/Core/Graphics/AnimationInfo.html) \

**Returns** \
[FrameInfo](../../Murder/Core/FrameInfo.html) \

#### DrawSprite(Batch2D, Vector2, Rectangle, string, SpriteAsset, float, float, bool, Vector2, ImageFlip, float, Vector2, Color, Vector3, MurderBlendState, float, float)

```csharp
public static FrameInfo DrawSprite(Batch2D spriteBatch, Vector2 pos, Rectangle clip, string animationId, SpriteAsset asset, float animationStartedTime, float animationDuration, bool animationLoop, Vector2 origin, ImageFlip imageFlip, float rotation, Vector2 scale, Color color, Vector3 blend, MurderBlendState blendState, float sort, float currentTime)
```

Renders a sprite with every low-level parameter exposed directly (clip rectangle, explicit animation timing/looping, blend vector and state, rotation, scale, etc.), computing the current frame from `currentTime - animationStartedTime` rather than an `AnimationInfo`. This is the most basic/most verbose rendering method in the class — avoid using it directly if one of the `DrawInfo`/`AnimationInfo`-based overloads covers your case, and prefer it only when you need to bypass those types entirely (e.g. custom animation timing not modeled by `AnimationInfo`).

**Parameters** \
`spriteBatch` [Batch2D](../../Murder/Core/Graphics/Batch2D.html) \
`pos` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`clip` [Rectangle](../../Murder/Core/Geometry/Rectangle.html) \
`animationId` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
`asset` [SpriteAsset](../../Murder/Assets/Graphics/SpriteAsset.html) \
`animationStartedTime` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`animationDuration` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`animationLoop` [bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
`origin` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`imageFlip` [ImageFlip](../../Murder/Core/Graphics/ImageFlip.html) \
`rotation` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`scale` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`color` [Color](../../Murder/Core/Graphics/Color.html) \
`blend` [Vector3](https://docs.monogame.net/api/Microsoft.Xna.Framework.Vector3.html) \
`blendState` [MurderBlendState](../../Murder/Core/Graphics/MurderBlendState.html) \
`sort` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`currentTime` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

**Returns** \
[FrameInfo](../../Murder/Core/FrameInfo.html) \

#### DrawSprite(Batch2D, Vector2, Rectangle, string, SpriteAsset, int, Vector2, ImageFlip, float, Vector2, Color, Vector3, float)

```csharp
public static FrameInfo DrawSprite(Batch2D spriteBatch, Vector2 pos, Rectangle clip, string animationId, SpriteAsset asset, int frame, Vector2 origin, ImageFlip imageFlip, float rotation, Vector2 scale, Color color, Vector3 blend, float sort)
```

Variant of the fully-exposed `DrawSprite` overload that draws an explicit `frame` index of `animationId` rather than evaluating a time-based animation — use when you need to pin a sprite to a specific frame (e.g. a paused/frozen animation, or a frame chosen by other game logic) instead of letting time drive it.

**Parameters** \
`spriteBatch` [Batch2D](../../Murder/Core/Graphics/Batch2D.html) \
`pos` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`clip` [Rectangle](../../Murder/Core/Geometry/Rectangle.html) \
`animationId` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
`asset` [SpriteAsset](../../Murder/Assets/Graphics/SpriteAsset.html) \
`frame` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`origin` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`imageFlip` [ImageFlip](../../Murder/Core/Graphics/ImageFlip.html) \
`rotation` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`scale` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`color` [Color](../../Murder/Core/Graphics/Color.html) \
`blend` [Vector3](https://docs.monogame.net/api/Microsoft.Xna.Framework.Vector3.html) \
`sort` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

**Returns** \
[FrameInfo](../../Murder/Core/FrameInfo.html) \

#### DrawSprite(Batch2D, Vector2, Rectangle, Animation, SpriteAsset, int, Vector2, ImageFlip, float, Vector2, Color, Vector3, float)

```csharp
public static FrameInfo DrawSprite(Batch2D spriteBatch, Vector2 pos, Rectangle clip, Animation animation, SpriteAsset asset, int frame, Vector2 origin, ImageFlip imageFlip, float rotation, Vector2 scale, Color color, Vector3 blend, float sort)
```

Like the explicit-frame overload above, but takes an already-resolved `Animation` instead of looking one up by name — used internally to avoid a redundant dictionary lookup once the animation is already known.

**Parameters** \
`spriteBatch` [Batch2D](../../Murder/Core/Graphics/Batch2D.html) \
`pos` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`clip` [Rectangle](../../Murder/Core/Geometry/Rectangle.html) \
`animation` [Animation](../../Murder/Core/Graphics/Animation.html) \
`asset` [SpriteAsset](../../Murder/Assets/Graphics/SpriteAsset.html) \
`frame` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`origin` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`imageFlip` [ImageFlip](../../Murder/Core/Graphics/ImageFlip.html) \
`rotation` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`scale` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`color` [Color](../../Murder/Core/Graphics/Color.html) \
`blend` [Vector3](https://docs.monogame.net/api/Microsoft.Xna.Framework.Vector3.html) \
`sort` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

**Returns** \
[FrameInfo](../../Murder/Core/FrameInfo.html) \

#### DrawSpriteAtRatio(Batch2D, SpriteAsset, Vector2, DrawInfo, string, float)

```csharp
public static FrameInfo DrawSpriteAtRatio(this Batch2D batch, SpriteAsset asset, Vector2 position, DrawInfo drawInfo, string animationName, float animationRatio)
```

Draws `animationName` from `asset` at whichever frame corresponds to `animationRatio` (`0` = first frame, `1` = last frame), instead of driving playback by elapsed time. Use for progress-linked animations — e.g. a loading spinner or a charge-up sprite tied to a 0-1 progress value rather than a clock.

**Parameters** \
`batch` [Batch2D](../../Murder/Core/Graphics/Batch2D.html) \
`asset` [SpriteAsset](../../Murder/Assets/Graphics/SpriteAsset.html) \
`position` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`drawInfo` [DrawInfo](../../Murder/Core/Graphics/DrawInfo.html) \
`animationName` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
`animationRatio` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

**Returns** \
[FrameInfo](../../Murder/Core/FrameInfo.html) \

#### DrawText(Batch2D, int, string, Vector2, DrawInfo?)

```csharp
public static Point DrawText(this Batch2D uiBatch, int font, string text, Vector2 position, DrawInfo? drawInfo = default)
```

Draws `text` (with line-wrapping and inline `<c=...>` color formatting support) at `position` using font index `font`, with no maximum width or character-reveal limit. Returns the rendered text's pixel size.

**Parameters** \
`uiBatch` [Batch2D](../../Murder/Core/Graphics/Batch2D.html) \
`font` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`text` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
`position` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`drawInfo` [DrawInfo?](../../Murder/Core/Graphics/DrawInfo.html) \

**Returns** \
[Point](../../Murder/Core/Geometry/Point.html) \

#### DrawText(Batch2D, int, string, Vector2, int, DrawInfo?)

```csharp
public static Point DrawText(this Batch2D uiBatch, int font, string text, Vector2 position, int maxWidth, DrawInfo? drawInfo = default)
```

Same as the width-less overload, but wraps lines at `maxWidth` pixels.

**Parameters** \
`uiBatch` [Batch2D](../../Murder/Core/Graphics/Batch2D.html) \
`font` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`text` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
`position` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`maxWidth` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`drawInfo` [DrawInfo?](../../Murder/Core/Graphics/DrawInfo.html) \

**Returns** \
[Point](../../Murder/Core/Geometry/Point.html) \

#### DrawText(Batch2D, int, string, Vector2, int, int, DrawInfo)

```csharp
public static Point DrawText(this Batch2D uiBatch, int pixelFont, string text, Vector2 position, int maxWidth, int visibleCharacters, DrawInfo drawInfo)
```

The core text-drawing routine every other `DrawText`/`DrawText(MurderFonts, ...)` overload eventually calls: wraps `text` at `maxWidth`, reveals only the first `visibleCharacters` characters (pass `-1` to reveal all — used for typewriter-style dialogue reveal), and draws it with `drawInfo`'s color/outline/shadow/origin.

**Parameters** \
`uiBatch` [Batch2D](../../Murder/Core/Graphics/Batch2D.html) \
`pixelFont` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`text` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
`position` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`maxWidth` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`visibleCharacters` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`drawInfo` [DrawInfo](../../Murder/Core/Graphics/DrawInfo.html) \

**Returns** \
[Point](../../Murder/Core/Geometry/Point.html) \

#### DrawText(Batch2D, MurderFonts, string, Vector2, DrawInfo?)

```csharp
public static Point DrawText(this Batch2D uiBatch, MurderFonts font, string text, Vector2 position, DrawInfo? drawInfo = default)
```

`MurderFonts`-enum overload of `DrawText(Batch2D, int, string, Vector2, DrawInfo?)`.

**Parameters** \
`uiBatch` [Batch2D](../../Murder/Core/Graphics/Batch2D.html) \
`font` [MurderFonts](../../Murder/Services/MurderFonts.html) \
`text` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
`position` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`drawInfo` [DrawInfo?](../../Murder/Core/Graphics/DrawInfo.html) \

**Returns** \
[Point](../../Murder/Core/Geometry/Point.html) \

#### DrawText(Batch2D, MurderFonts, string, Vector2, int, DrawInfo?)

```csharp
public static Point DrawText(this Batch2D uiBatch, MurderFonts font, string text, Vector2 position, int maxWidth, DrawInfo? drawInfo = default)
```

`MurderFonts`-enum overload of `DrawText(Batch2D, int, string, Vector2, int, DrawInfo?)`.

**Parameters** \
`uiBatch` [Batch2D](../../Murder/Core/Graphics/Batch2D.html) \
`font` [MurderFonts](../../Murder/Services/MurderFonts.html) \
`text` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
`position` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`maxWidth` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`drawInfo` [DrawInfo?](../../Murder/Core/Graphics/DrawInfo.html) \

**Returns** \
[Point](../../Murder/Core/Geometry/Point.html) \

#### DrawText(Batch2D, MurderFonts, string, Vector2, int, int, DrawInfo?)

```csharp
public static Point DrawText(this Batch2D uiBatch, MurderFonts font, string text, Vector2 position, int maxWidth, int visibleCharacters, DrawInfo? drawInfo = default)
```

`MurderFonts`-enum overload that also supports the typewriter-style `visibleCharacters` reveal limit.

**Parameters** \
`uiBatch` [Batch2D](../../Murder/Core/Graphics/Batch2D.html) \
`font` [MurderFonts](../../Murder/Services/MurderFonts.html) \
`text` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
`position` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`maxWidth` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`visibleCharacters` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`drawInfo` [DrawInfo?](../../Murder/Core/Graphics/DrawInfo.html) \

**Returns** \
[Point](../../Murder/Core/Geometry/Point.html) \

#### DrawTexture(Batch2D, Texture2D, Vector2, DrawInfo)

```csharp
public static void DrawTexture(this Batch2D batch, Texture2D texture, Vector2 position, DrawInfo drawInfo)
```

Draws a raw `Texture2D` (not an atlas-packed sprite) at `position`, honoring `drawInfo`'s clip/origin/scale/rotation/color and drawing an outline pass first if `drawInfo.Outline` is set. Use for one-off, non-atlased textures — e.g. a dynamically generated texture or a screenshot captured via `CreateScreenshot`.

**Parameters** \
`batch` [Batch2D](../../Murder/Core/Graphics/Batch2D.html) \
`texture` [Texture2D](https://docs.monogame.net/api/Microsoft.Xna.Framework.Graphics.Texture2D.html) \
`position` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`drawInfo` [DrawInfo](../../Murder/Core/Graphics/DrawInfo.html) \

#### DrawTextureQuad(Texture2D, Rectangle, Rectangle, Color, BlendState)

```csharp
public static void DrawTextureQuad(Texture2D texture, Rectangle source, Rectangle destination, Color color, BlendState blend)
```

Blits `source` region of `texture` into `destination`, selecting the engine's built-in sprite shader's "Add" or "Alpha" technique based on `blend`.

**Parameters** \
`texture` [Texture2D](https://docs.monogame.net/api/Microsoft.Xna.Framework.Graphics.Texture2D.html) \
`source` [Rectangle](../../Murder/Core/Geometry/Rectangle.html) \
`destination` [Rectangle](../../Murder/Core/Geometry/Rectangle.html) \
`color` [Color](../../Murder/Core/Graphics/Color.html) \
`blend` [BlendState](https://docs.monogame.net/api/Microsoft.Xna.Framework.Graphics.BlendState.html) \

#### DrawTextureQuad(Texture2D, Rectangle, Rectangle, Color, BlendState, Effect)

```csharp
public static void DrawTextureQuad(Texture2D texture, Rectangle source, Rectangle destination, Color color, BlendState blend, Effect? shaderEffect)
```

Blits `source` into `destination` using an explicit `shaderEffect` instead of the engine's default sprite shader.

**Parameters** \
`texture` [Texture2D](https://docs.monogame.net/api/Microsoft.Xna.Framework.Graphics.Texture2D.html) \
`source` [Rectangle](../../Murder/Core/Geometry/Rectangle.html) \
`destination` [Rectangle](../../Murder/Core/Geometry/Rectangle.html) \
`color` [Color](../../Murder/Core/Graphics/Color.html) \
`blend` [BlendState](https://docs.monogame.net/api/Microsoft.Xna.Framework.Graphics.BlendState.html) \
`shaderEffect` [Effect](https://docs.monogame.net/api/Microsoft.Xna.Framework.Graphics.Effect.html) \

#### DrawTextureQuad(Texture2D, Rectangle, Rectangle, Color, BlendState, Effect, Vector3)

```csharp
public static void DrawTextureQuad(Texture2D texture, Rectangle source, Rectangle destination, Color color, BlendState blend, Effect? shaderEffect, Vector3 colorBlend)
```

Full-control blit overload: lets the caller also specify the `colorBlend` vector (normal/wash/color-only tinting) alongside a custom `shaderEffect` and `blend` state.

**Parameters** \
`texture` [Texture2D](https://docs.monogame.net/api/Microsoft.Xna.Framework.Graphics.Texture2D.html) \
`source` [Rectangle](../../Murder/Core/Geometry/Rectangle.html) \
`destination` [Rectangle](../../Murder/Core/Geometry/Rectangle.html) \
`color` [Color](../../Murder/Core/Graphics/Color.html) \
`blend` [BlendState](https://docs.monogame.net/api/Microsoft.Xna.Framework.Graphics.BlendState.html) \
`shaderEffect` [Effect](https://docs.monogame.net/api/Microsoft.Xna.Framework.Graphics.Effect.html) \
`colorBlend` [Vector3](https://docs.monogame.net/api/Microsoft.Xna.Framework.Vector3.html) \

#### DrawTextureQuad(Texture2D, Rectangle, Rectangle, Color, Effect, BlendState, bool)

```csharp
public static void DrawTextureQuad(Texture2D texture, Rectangle source, Rectangle destination, Color color, Effect? effect, BlendState blend, bool smoothing)
```

Blits `source` into `destination` with explicit control over point-vs-linear `smoothing`, always tinting with `BLEND_NORMAL`. Used when the caller needs texture smoothing control that the other `DrawTextureQuad` overloads don't expose.

**Parameters** \
`texture` [Texture2D](https://docs.monogame.net/api/Microsoft.Xna.Framework.Graphics.Texture2D.html) \
`source` [Rectangle](../../Murder/Core/Geometry/Rectangle.html) \
`destination` [Rectangle](../../Murder/Core/Geometry/Rectangle.html) \
`color` [Color](../../Murder/Core/Graphics/Color.html) \
`effect` [Effect](https://docs.monogame.net/api/Microsoft.Xna.Framework.Graphics.Effect.html) \
`blend` [BlendState](https://docs.monogame.net/api/Microsoft.Xna.Framework.Graphics.BlendState.html) \
`smoothing` [bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### DrawTriangle(Batch2D, Vector2, float, float, DrawInfo)

```csharp
public static void DrawTriangle(this Batch2D batch, Vector2 position, float radius, float rotation, DrawInfo drawInfo)
```

Draws a filled equilateral triangle centred at `position` with the given `radius` and `rotation`, built from `GeometryServices.GetTriangle` and drawn via `DrawPolygon`.

**Parameters** \
`batch` [Batch2D](../../Murder/Core/Graphics/Batch2D.html) \
`position` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`radius` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`rotation` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`drawInfo` [DrawInfo](../../Murder/Core/Graphics/DrawInfo.html) \

#### DrawVerticalLine(Batch2D, int, int, int, Color, float)

```csharp
public static void DrawVerticalLine(this Batch2D spriteBatch, int x, int y, int length, Color color, float sorting = 0)
```

Draws a single-pixel-wide vertical line of `length` pixels starting at `(x, y)`.

**Parameters** \
`spriteBatch` [Batch2D](../../Murder/Core/Graphics/Batch2D.html) \
`x` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`y` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`length` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`color` [Color](../../Murder/Core/Graphics/Color.html) \
`sorting` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### DrawVerticalMenu(Batch2D, Point, DrawMenuStyle, MenuInfo, float)

```csharp
public static DrawMenuInfo DrawVerticalMenu(Batch2D batch, in Point position, in DrawMenuStyle style, in MenuInfo menuInfo, float sort = .1f)
```

Draws `menuInfo`'s options as a vertical list at `position` (both the option text and the selector use the same origin), returning the computed `DrawMenuInfo` layout. Convenience overload of `DrawVerticalMenu(Batch2D, Point, Point, DrawMenuStyle, MenuInfo, float)` for the common case where the selector and text share one anchor point.

**Parameters** \
`batch` [Batch2D](../../Murder/Core/Graphics/Batch2D.html) \
`position` [Point](../../Murder/Core/Geometry/Point.html) \
`style` [DrawMenuStyle](../../Murder/Services/DrawMenuStyle.html) \
`menuInfo` [MenuInfo](../../Murder/Core/Input/MenuInfo.html) \
`sort` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

**Returns** \
[DrawMenuInfo](../../Murder/Services/Info/DrawMenuInfo.html) \

#### DrawVerticalMenu(Batch2D, Point, Point, DrawMenuStyle, MenuInfo, float)

```csharp
public static DrawMenuInfo DrawVerticalMenu(Batch2D batch, in Point position, in Point textPosition, in DrawMenuStyle style, in MenuInfo menuInfo, float sort)
```

Draws each `MenuOption` in `menuInfo` as one row of a vertical list — label text at `textPosition`, selector cursor anchored at `position` — using `style`'s font/colors/spacing/animation settings, and optionally an icon per option (from `menuInfo.Icons`) when the style's origin is left-aligned. Returns a `DrawMenuInfo` with the computed selector/eased positions and row metrics for the caller to draw additional decoration with. This is the primary way to render a simple interactive menu in Murder without hand-rolling per-option layout.

**Parameters** \
`batch` [Batch2D](../../Murder/Core/Graphics/Batch2D.html) \
`position` [Point](../../Murder/Core/Geometry/Point.html) \
`textPosition` [Point](../../Murder/Core/Geometry/Point.html) \
`style` [DrawMenuStyle](../../Murder/Services/DrawMenuStyle.html) \
`menuInfo` [MenuInfo](../../Murder/Core/Input/MenuInfo.html) \
`sort` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

**Returns** \
[DrawMenuInfo](../../Murder/Services/Info/DrawMenuInfo.html) \

#### FetchPortraitAsSprite(Portrait)

```csharp
public static (SpriteAsset asset, string animation)? FetchPortraitAsSprite(Portrait portrait)
```

Resolves `portrait.Sprite` to its loaded `SpriteAsset`, returning it paired with `portrait.AnimationId`, or `null` if the sprite asset isn't loaded. Used by `DrawPortrait` and useful directly whenever code needs the underlying sprite/animation pair without immediately drawing it (e.g. to measure it first).

**Parameters** \
`portrait` [Portrait](../../Murder/Core/Portrait.html) \

**Returns** \
[(SpriteAsset, string)?](../../Murder/Assets/Graphics/SpriteAsset.html) \

#### GetSharedQuad(Rectangle, Rectangle, Vector2, Color, Vector3)

```csharp
public static (VertexInfo[] vertices, short[] indices) GetSharedQuad(Rectangle destination, Rectangle source, Vector2 sourceSize, Color color, Vector3 BlendType)
```

Builds (into a shared, reused vertex/index buffer — not a fresh allocation) the four vertices and six indices needed to draw `source` (in UV space, relative to `sourceSize`) blitted into `destination`. The vertex-building primitive behind `DrawTextureQuad`; only useful directly if you're implementing custom textured-quad rendering.

**Parameters** \
`destination` [Rectangle](../../Murder/Core/Geometry/Rectangle.html) \
`source` [Rectangle](../../Murder/Core/Geometry/Rectangle.html) \
`sourceSize` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`color` [Color](../../Murder/Core/Graphics/Color.html) \
`BlendType` [Vector3](https://docs.monogame.net/api/Microsoft.Xna.Framework.Vector3.html) \

**Returns** \
[(VertexInfo[], short[])](../../Murder/Core/Graphics/VertexInfo.html) \

#### MessageCompleteAnimations(Entity)

```csharp
public static void MessageCompleteAnimations(Entity e)
```

Marks `e`'s current animation as complete and sends the complete message, additionally clearing any `AnimationOverloadComponent` if it isn't set to loop. Called when a system needs to force-finish whatever animation is currently playing on `e` — for example when gameplay is paused and animations must be flushed to a resting/complete state (see `AnimationOnPauseSystem`).

**Parameters** \
`e` [Entity](../../Bang/Entities/Entity.html) \

#### TriggerEventsIfNeeded(Entity, Guid, AnimationInfo, FrameInfo, AnimationEventsTriggerFlag)

```csharp
public static bool TriggerEventsIfNeeded(Entity e, Guid currentAnimationGuid, AnimationInfo animationInfo, FrameInfo frameInfo, AnimationEventsTriggerFlag flags)
```

Compares the animation frame rendered this call (`frameInfo`) against the frame recorded in `e`'s `RenderedSpriteCacheComponent` from the previous call, and sends an `AnimationEventMessage` for every named frame event crossed in between (handling both looping and, with `AnimationEventsTriggerFlag.AllowReverse`, backwards-playing animations). This is the primitive that lets sprite-driven animation events (e.g. "spawn a hit VFX on frame 4") fire reliably even if a frame is skipped due to a slow frame. Called every frame by the sprite-rendering systems (`SpriteRenderSystem`, `AgentSpriteSystem`, `SpriteAtRatioRenderSystem`); not typically called directly by gameplay code.

**Parameters** \
`e` [Entity](../../Bang/Entities/Entity.html) \
`currentAnimationGuid` [Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \
`animationInfo` [AnimationInfo](../../Murder/Core/Graphics/AnimationInfo.html) \
`frameInfo` [FrameInfo](../../Murder/Core/FrameInfo.html) \
`flags` [AnimationEventsTriggerFlag](../../Murder/Components/Graphics/AnimationEventsTriggerFlag.html) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### ToVector3(BlendStyle)

```csharp
public static Vector3 ToVector3(this BlendStyle blendStyle)
```

Converts a `BlendStyle` enum value (`Normal`/`Wash`/`Color`) to the corresponding raw `Vector3` blend vector (`BLEND_NORMAL`/`BLEND_WASH`/`BLEND_COLOR_ONLY`) the shaders expect; throws if given an unsupported value. Used when a `DrawInfo`'s higher-level `BlendStyle` needs to be converted to the vector the batch/shader pipeline actually consumes.

**Parameters** \
`blendStyle` [BlendStyle](../../Murder/Core/Graphics/BlendStyle.html) \

**Returns** \
[Vector3](https://docs.monogame.net/api/Microsoft.Xna.Framework.Vector3.html) \

#### UpdateRenderedSpriteCache(Entity, RenderedSpriteCache)

```csharp
public static void UpdateRenderedSpriteCache(Entity e, RenderedSpriteCache cache)
```

Updates `e`'s `RenderedSpriteCacheComponent` in place (via a `Ref` to avoid a full component replacement every frame) if it exists, or creates one otherwise. Used by the sprite-rendering systems to remember which frame was last rendered, so `TriggerEventsIfNeeded` can detect frame crossings on the next call. A performance-motivated helper (see the source comment) — not typically called from gameplay code.

**Parameters** \
`e` [Entity](../../Bang/Entities/Entity.html) \
`cache` [RenderedSpriteCache](../../Murder/Components/Graphics/RenderedSpriteCache.html) \

#### YSort(float)

```csharp
public static float YSort(float y)
```

Converts a world-space Y coordinate into a normalized `[0, 1]`-ish depth-sort value (lower Y sorts in front) suitable for `DrawInfo.Sort`/`Batch2D`'s depth ordering, so sprites naturally draw back-to-front by their vertical position.

**Parameters** \
`y` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

⚡
