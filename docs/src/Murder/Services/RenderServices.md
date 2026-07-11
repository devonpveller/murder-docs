# RenderServices

**Namespace:** Murder.Services \
**Assembly:** Murder.dll

```csharp
public static class RenderServices
```

Core rendering utility class providing methods for drawing sprites, shapes, text, and UI elements to a `Batch2D`.

**Intent:** Centralises all 2D drawing operations so game systems and interactions can render content without directly managing batches or atlases.

**Use-case:** Call the `DrawSprite` family to render animated sprites, `DrawText`/`DrawSimpleText` for labels, `Draw9Slice` for scalable UI panels, and shape primitives (`DrawLine`, `DrawRectangle`, etc.) for debug or gameplay overlays.

### ⭐ Properties
#### BLEND_COLOR_ONLY
```csharp
public static Vector3 BLEND_COLOR_ONLY;
```
Blend vector that applies only the color channel while discarding the original sprite colors (tint-only mode).

**Returns** \
[Vector3](https://docs.monogame.net/api/Microsoft.Xna.Framework.Vector3.html) \
#### BLEND_NORMAL
```csharp
public static Vector3 BLEND_NORMAL;
```
Default blend vector that draws the sprite with its original colors unchanged.

**Returns** \
[Vector3](https://docs.monogame.net/api/Microsoft.Xna.Framework.Vector3.html) \
#### BLEND_WASH
```csharp
public static Vector3 BLEND_WASH;
```
Blend vector that washes the sprite toward the tint color, mixing original and tint hues.

**Returns** \
[Vector3](https://docs.monogame.net/api/Microsoft.Xna.Framework.Vector3.html) \
### ⭐ Methods
#### DrawVerticalMenu(Batch2D, Point&, Point&, DrawMenuStyle&, MenuInfo&)
```csharp
public DrawMenuInfo DrawVerticalMenu(Batch2D batch, Point& position, Point& textPosition, DrawMenuStyle& style, MenuInfo& menuInfo)
```
Draws a vertical list of menu options, returning layout info such as the final drawn position and selected item bounds.

**Parameters** \
`batch` [Batch2D](../../Murder/Core/Graphics/Batch2D.html) \
`position` [Point&](../../Murder/Core/Geometry/Point.html) \
`textPosition` [Point&](../../Murder/Core/Geometry/Point.html) \
`style` [DrawMenuStyle&](../../Murder/Services/DrawMenuStyle.html) \
`menuInfo` [MenuInfo&](../../Murder/Core/Input/MenuInfo.html) \

**Returns** \
[DrawMenuInfo](../../Murder/Services/Info/DrawMenuInfo.html) \

#### DrawVerticalMenu(Batch2D, Point&, DrawMenuStyle&, MenuInfo&)
```csharp
public DrawMenuInfo DrawVerticalMenu(Batch2D batch, Point& position, DrawMenuStyle& style, MenuInfo& menuInfo)
```
Draws a vertical list of menu options with text and selector positions collapsed to a single origin.

**Parameters** \
`batch` [Batch2D](../../Murder/Core/Graphics/Batch2D.html) \
`position` [Point&](../../Murder/Core/Geometry/Point.html) \
`style` [DrawMenuStyle&](../../Murder/Services/DrawMenuStyle.html) \
`menuInfo` [MenuInfo&](../../Murder/Core/Input/MenuInfo.html) \

**Returns** \
[DrawMenuInfo](../../Murder/Services/Info/DrawMenuInfo.html) \

#### CurrentTime(AnimationInfo)
```csharp
public float CurrentTime(AnimationInfo this)
```

Fetch the current time for this animation.

**Parameters** \
`this` [AnimationInfo](../../Murder/Core/Graphics/AnimationInfo.html) \

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### YSort(float)
```csharp
public float YSort(float y)
```
Converts a world-space Y coordinate to a normalized depth-sort value for correct depth ordering in the render batch.

**Parameters** \
`y` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### DrawPortrait(Batch2D, Portrait, Vector2, DrawInfo)
```csharp
public FrameInfo DrawPortrait(Batch2D batch, Portrait portrait, Vector2 position, DrawInfo drawInfo)
```
Draws a portrait sprite (a named animation from a sprite asset) at `position` and returns the rendered frame information.

**Parameters** \
`batch` [Batch2D](../../Murder/Core/Graphics/Batch2D.html) \
`portrait` [Portrait](../../Murder/Core/Portrait.html) \
`position` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`drawInfo` [DrawInfo](../../Murder/Core/Graphics/DrawInfo.html) \

**Returns** \
[FrameInfo](../../Murder/Core/FrameInfo.html) \

#### DrawSprite(Batch2D, SpriteAsset, Vector2, DrawInfo, AnimationInfo)
```csharp
public FrameInfo DrawSprite(Batch2D batch, SpriteAsset asset, Vector2 position, DrawInfo drawInfo, AnimationInfo animationInfo)
```
Draws a sprite asset at `position` using the specified draw and animation parameters.

**Parameters** \
`batch` [Batch2D](../../Murder/Core/Graphics/Batch2D.html) \
`asset` [SpriteAsset](../../Murder/Assets/Graphics/SpriteAsset.html) \
`position` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`drawInfo` [DrawInfo](../../Murder/Core/Graphics/DrawInfo.html) \
`animationInfo` [AnimationInfo](../../Murder/Core/Graphics/AnimationInfo.html) \

**Returns** \
[FrameInfo](../../Murder/Core/FrameInfo.html) \

#### DrawSprite(Batch2D, SpriteAsset, Vector2, T?)
```csharp
public FrameInfo DrawSprite(Batch2D batch, SpriteAsset asset, Vector2 position, T? drawInfo)
```
Draws a sprite asset at `position` using optional draw parameters (null uses defaults).

**Parameters** \
`batch` [Batch2D](../../Murder/Core/Graphics/Batch2D.html) \
`asset` [SpriteAsset](../../Murder/Assets/Graphics/SpriteAsset.html) \
`position` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`drawInfo` [T?](https://learn.microsoft.com/en-us/dotnet/api/System.Nullable-1?view=net-7.0) \

**Returns** \
[FrameInfo](../../Murder/Core/FrameInfo.html) \

#### DrawSprite(Batch2D, Guid, float, float, DrawInfo, AnimationInfo)
```csharp
public FrameInfo DrawSprite(Batch2D batch, Guid assetGuid, float x, float y, DrawInfo drawInfo, AnimationInfo animationInfo)
```
Draws the sprite asset identified by `assetGuid` at pixel coordinates `(x, y)`.

**Parameters** \
`batch` [Batch2D](../../Murder/Core/Graphics/Batch2D.html) \
`assetGuid` [Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \
`x` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`y` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`drawInfo` [DrawInfo](../../Murder/Core/Graphics/DrawInfo.html) \
`animationInfo` [AnimationInfo](../../Murder/Core/Graphics/AnimationInfo.html) \

**Returns** \
[FrameInfo](../../Murder/Core/FrameInfo.html) \

#### DrawSprite(Batch2D, Guid, Vector2, DrawInfo, AnimationInfo)
```csharp
public FrameInfo DrawSprite(Batch2D batch, Guid assetGuid, Vector2 position, DrawInfo drawInfo, AnimationInfo animationInfo)
```
Draws the sprite asset identified by `assetGuid` at `position`.

**Parameters** \
`batch` [Batch2D](../../Murder/Core/Graphics/Batch2D.html) \
`assetGuid` [Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \
`position` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`drawInfo` [DrawInfo](../../Murder/Core/Graphics/DrawInfo.html) \
`animationInfo` [AnimationInfo](../../Murder/Core/Graphics/AnimationInfo.html) \

**Returns** \
[FrameInfo](../../Murder/Core/FrameInfo.html) \

#### DrawSprite(Batch2D, Guid, Vector2, T?)
```csharp
public FrameInfo DrawSprite(Batch2D batch, Guid assetGuid, Vector2 position, T? drawInfo)
```
Draws the sprite asset identified by `assetGuid` at `position` with optional draw parameters.

**Parameters** \
`batch` [Batch2D](../../Murder/Core/Graphics/Batch2D.html) \
`assetGuid` [Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \
`position` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`drawInfo` [T?](https://learn.microsoft.com/en-us/dotnet/api/System.Nullable-1?view=net-7.0) \

**Returns** \
[FrameInfo](../../Murder/Core/FrameInfo.html) \

#### DrawSprite(Batch2D, Vector2, Rectangle, string, SpriteAsset, float, float, bool, Vector2, ImageFlip, float, Vector2, Color, Vector3, float, float)
```csharp
public FrameInfo DrawSprite(Batch2D spriteBatch, Vector2 pos, Rectangle clip, string animationId, SpriteAsset asset, float animationStartedTime, float animationDuration, bool animationLoop, Vector2 origin, ImageFlip imageFlip, float rotation, Vector2 scale, Color color, Vector3 blend, float sort, float currentTime)
```

The Renders a sprite on the screen. This is the most basic rendering method with all parameters exposed, avoid using this if possible.

**Parameters** \
`spriteBatch` [Batch2D](../../Murder/Core/Graphics/Batch2D.html) \
\
`pos` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
\
`clip` [Rectangle](../../Murder/Core/Geometry/Rectangle.html) \
\
`animationId` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
\
`asset` [SpriteAsset](../../Murder/Assets/Graphics/SpriteAsset.html) \
\
`animationStartedTime` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
\
`animationDuration` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
\
`animationLoop` [bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
\
`origin` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
\
`imageFlip` [ImageFlip](../../Murder/Core/Graphics/ImageFlip.html) \
\
`rotation` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
\
`scale` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
\
`color` [Color](../../Murder/Core/Graphics/Color.html) \
\
`blend` [Vector3](https://docs.monogame.net/api/Microsoft.Xna.Framework.Vector3.html) \
\
`sort` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
\
`currentTime` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
\

**Returns** \
[FrameInfo](../../Murder/Core/FrameInfo.html) \
\

#### DrawSimpleText(Batch2D, int, string, Vector2, DrawInfo)
```csharp
public Point DrawSimpleText(Batch2D uiBatch, int pixelFont, string text, Vector2 position, DrawInfo drawInfo)
```

Draw a simple text. Without line wrapping, color formatting, line splitting or anything fancy.

**Parameters** \
`uiBatch` [Batch2D](../../Murder/Core/Graphics/Batch2D.html) \
`pixelFont` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`text` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
`position` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`drawInfo` [DrawInfo](../../Murder/Core/Graphics/DrawInfo.html) \

**Returns** \
[Point](../../Murder/Core/Geometry/Point.html) \

#### DrawText(Batch2D, MurderFonts, string, Vector2, int, int, T?)
```csharp
public Point DrawText(Batch2D uiBatch, MurderFonts font, string text, Vector2 position, int maxWidth, int visibleCharacters, T? drawInfo)
```

**Parameters** \
`uiBatch` [Batch2D](../../Murder/Core/Graphics/Batch2D.html) \
`font` [MurderFonts](../../Murder/Services/MurderFonts.html) \
`text` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
`position` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`maxWidth` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`visibleCharacters` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`drawInfo` [T?](https://learn.microsoft.com/en-us/dotnet/api/System.Nullable-1?view=net-7.0) \

**Returns** \
[Point](../../Murder/Core/Geometry/Point.html) \

#### DrawText(Batch2D, MurderFonts, string, Vector2, int, T?)
```csharp
public Point DrawText(Batch2D uiBatch, MurderFonts font, string text, Vector2 position, int maxWidth, T? drawInfo)
```

**Parameters** \
`uiBatch` [Batch2D](../../Murder/Core/Graphics/Batch2D.html) \
`font` [MurderFonts](../../Murder/Services/MurderFonts.html) \
`text` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
`position` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`maxWidth` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`drawInfo` [T?](https://learn.microsoft.com/en-us/dotnet/api/System.Nullable-1?view=net-7.0) \

**Returns** \
[Point](../../Murder/Core/Geometry/Point.html) \

#### DrawText(Batch2D, MurderFonts, string, Vector2, T?)
```csharp
public Point DrawText(Batch2D uiBatch, MurderFonts font, string text, Vector2 position, T? drawInfo)
```

**Parameters** \
`uiBatch` [Batch2D](../../Murder/Core/Graphics/Batch2D.html) \
`font` [MurderFonts](../../Murder/Services/MurderFonts.html) \
`text` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
`position` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`drawInfo` [T?](https://learn.microsoft.com/en-us/dotnet/api/System.Nullable-1?view=net-7.0) \

**Returns** \
[Point](../../Murder/Core/Geometry/Point.html) \

#### DrawText(Batch2D, int, string, Vector2, int, T?)
```csharp
public Point DrawText(Batch2D uiBatch, int font, string text, Vector2 position, int maxWidth, T? drawInfo)
```

**Parameters** \
`uiBatch` [Batch2D](../../Murder/Core/Graphics/Batch2D.html) \
`font` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`text` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
`position` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`maxWidth` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`drawInfo` [T?](https://learn.microsoft.com/en-us/dotnet/api/System.Nullable-1?view=net-7.0) \

**Returns** \
[Point](../../Murder/Core/Geometry/Point.html) \

#### DrawText(Batch2D, int, string, Vector2, T?)
```csharp
public Point DrawText(Batch2D uiBatch, int font, string text, Vector2 position, T? drawInfo)
```

**Parameters** \
`uiBatch` [Batch2D](../../Murder/Core/Graphics/Batch2D.html) \
`font` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`text` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
`position` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`drawInfo` [T?](https://learn.microsoft.com/en-us/dotnet/api/System.Nullable-1?view=net-7.0) \

**Returns** \
[Point](../../Murder/Core/Geometry/Point.html) \

#### DrawText(Batch2D, int, string, Vector2, int, int, DrawInfo)
```csharp
public Point DrawText(Batch2D uiBatch, int pixelFont, string text, Vector2 position, int maxWidth, int visibleCharacters, DrawInfo drawInfo)
```

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

#### FetchPortraitAsSprite(Portrait)
```csharp
public T? FetchPortraitAsSprite(Portrait portrait)
```
Returns the `AtlasCoordinates` for a portrait's current animation frame, or `null` if the asset is not loaded.

**Parameters** \
`portrait` [Portrait](../../Murder/Core/Portrait.html) \

**Returns** \
[T?](https://learn.microsoft.com/en-us/dotnet/api/System.Nullable-1?view=net-7.0) \

#### CreateGameplayScreenShot()
```csharp
public Texture2D CreateGameplayScreenShot()
```

Don't forget to dispose this!

**Returns** \
[Texture2D](https://docs.monogame.net/api/Microsoft.Xna.Framework.Graphics.Texture2D.html) \
\

#### Draw3Slice(Batch2D, AtlasCoordinates, Rectangle, Vector2, Vector2, Vector2, Orientation, float)
```csharp
public void Draw3Slice(Batch2D batch, AtlasCoordinates texture, Rectangle core, Vector2 position, Vector2 size, Vector2 origin, Orientation orientation, float sort)
```
Draws a three-slice (horizontal or vertical) stretched texture between `position` and `size` using `core` as the fixed center region.

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
public void Draw9Slice(Batch2D batch, AtlasCoordinates texture, IntRectangle core, IntRectangle target, NineSliceStyle style, DrawInfo info)
```
Draws a nine-slice scalable UI element stretching `texture` to fill `target` while keeping the `core` corners unstretched.

**Parameters** \
`batch` [Batch2D](../../Murder/Core/Graphics/Batch2D.html) \
`texture` [AtlasCoordinates](../../Murder/Core/Graphics/AtlasCoordinates.html) \
`core` [IntRectangle](../../Murder/Core/Geometry/IntRectangle.html) \
`target` [IntRectangle](../../Murder/Core/Geometry/IntRectangle.html) \
`style` [NineSliceStyle](../../Murder/Core/Graphics/NineSliceStyle.html) \
`info` [DrawInfo](../../Murder/Core/Graphics/DrawInfo.html) \

#### Draw9Slice(Batch2D, AtlasCoordinates, Rectangle, Rectangle, float)
```csharp
public void Draw9Slice(Batch2D batch, AtlasCoordinates texture, Rectangle core, Rectangle target, float sort)
```
Draws a nine-slice element using float rectangles for the core and target regions.

**Parameters** \
`batch` [Batch2D](../../Murder/Core/Graphics/Batch2D.html) \
`texture` [AtlasCoordinates](../../Murder/Core/Graphics/AtlasCoordinates.html) \
`core` [Rectangle](../../Murder/Core/Geometry/Rectangle.html) \
`target` [Rectangle](../../Murder/Core/Geometry/Rectangle.html) \
`sort` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### Draw9Slice(Batch2D, Guid, Rectangle, DrawInfo, AnimationInfo)
```csharp
public void Draw9Slice(Batch2D batch, Guid guid, Rectangle target, DrawInfo drawInfo, AnimationInfo animationInfo)
```

Draws a 9-slice using the given texture and target rectangle. The core rectangle is specified in the Aseprite file

**Parameters** \
`batch` [Batch2D](../../Murder/Core/Graphics/Batch2D.html) \
`guid` [Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \
`target` [Rectangle](../../Murder/Core/Geometry/Rectangle.html) \
`drawInfo` [DrawInfo](../../Murder/Core/Graphics/DrawInfo.html) \
`animationInfo` [AnimationInfo](../../Murder/Core/Graphics/AnimationInfo.html) \

#### Draw9Slice(Batch2D, Guid, Rectangle, DrawInfo)
```csharp
public void Draw9Slice(Batch2D batch, Guid guid, Rectangle target, DrawInfo drawInfo)
```

Draws a 9-slice using the given texture and target rectangle. The core rectangle is specified in the Aseprite file

**Parameters** \
`batch` [Batch2D](../../Murder/Core/Graphics/Batch2D.html) \
`guid` [Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \
`target` [Rectangle](../../Murder/Core/Geometry/Rectangle.html) \
`drawInfo` [DrawInfo](../../Murder/Core/Graphics/DrawInfo.html) \

#### Draw9Slice(Batch2D, Guid, Rectangle, NineSliceStyle, DrawInfo, AnimationInfo)
```csharp
public void Draw9Slice(Batch2D batch, Guid guid, Rectangle target, NineSliceStyle style, DrawInfo drawInfo, AnimationInfo animationInfo)
```

Draws a 9-slice using the given texture and target rectangle. The core rectangle is specified in the Aseprite file

**Parameters** \
`batch` [Batch2D](../../Murder/Core/Graphics/Batch2D.html) \
`guid` [Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \
`target` [Rectangle](../../Murder/Core/Geometry/Rectangle.html) \
`style` [NineSliceStyle](../../Murder/Core/Graphics/NineSliceStyle.html) \
`drawInfo` [DrawInfo](../../Murder/Core/Graphics/DrawInfo.html) \
`animationInfo` [AnimationInfo](../../Murder/Core/Graphics/AnimationInfo.html) \

#### Draw9SliceWithText(Batch2D, Guid, string, int, Rectangle, DrawInfo, DrawInfo, AnimationInfo)
```csharp
public void Draw9SliceWithText(Batch2D batch, Guid sprite, string text, int font, Rectangle target, DrawInfo textDrawInfo, DrawInfo sliceDrawInfo, AnimationInfo sliceAnimationInfo)
```
Draws a nine-slice sprite and renders `text` centered inside it.

**Parameters** \
`batch` [Batch2D](../../Murder/Core/Graphics/Batch2D.html) \
`sprite` [Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \
`text` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
`font` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`target` [Rectangle](../../Murder/Core/Geometry/Rectangle.html) \
`textDrawInfo` [DrawInfo](../../Murder/Core/Graphics/DrawInfo.html) \
`sliceDrawInfo` [DrawInfo](../../Murder/Core/Graphics/DrawInfo.html) \
`sliceAnimationInfo` [AnimationInfo](../../Murder/Core/Graphics/AnimationInfo.html) \

#### DrawArrow(Batch2D, Vector2, Vector2, Color, float, float, float)
```csharp
public void DrawArrow(Batch2D spriteBatch, Vector2 point1, Vector2 point2, Color color, float thickness, float headSize, float sort)
```
Draws an arrow from `point1` to `point2` with a filled arrowhead of size `headSize`.

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
public void DrawCircleOutline(Batch2D spriteBatch, Point center, float radius, int sides, Color color, float sort)
```
Draws a wireframe circle centred at `center` (integer point overload).

**Parameters** \
`spriteBatch` [Batch2D](../../Murder/Core/Graphics/Batch2D.html) \
`center` [Point](../../Murder/Core/Geometry/Point.html) \
`radius` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`sides` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`color` [Color](../../Murder/Core/Graphics/Color.html) \
`sort` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### DrawCircleOutline(Batch2D, Rectangle, int, Color)
```csharp
public void DrawCircleOutline(Batch2D spriteBatch, Rectangle rectangle, int sides, Color color)
```
Draws a wireframe ellipse inscribed within `rectangle`.

**Parameters** \
`spriteBatch` [Batch2D](../../Murder/Core/Graphics/Batch2D.html) \
`rectangle` [Rectangle](../../Murder/Core/Geometry/Rectangle.html) \
`sides` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`color` [Color](../../Murder/Core/Graphics/Color.html) \

#### DrawCircleOutline(Batch2D, Vector2, float, int, Color, float)
```csharp
public void DrawCircleOutline(Batch2D spriteBatch, Vector2 center, float radius, int sides, Color color, float sort)
```

Draw a circle

**Parameters** \
`spriteBatch` [Batch2D](../../Murder/Core/Graphics/Batch2D.html) \
\
`center` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
\
`radius` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
\
`sides` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
\
`color` [Color](../../Murder/Core/Graphics/Color.html) \
\
`sort` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
\

#### DrawFilledCircle(Batch2D, Rectangle, int, DrawInfo)
```csharp
public void DrawFilledCircle(Batch2D batch, Rectangle circleRect, int steps, DrawInfo drawInfo)
```
Draws a filled circle (approximated as a polygon) inscribed within `circleRect`.

**Parameters** \
`batch` [Batch2D](../../Murder/Core/Graphics/Batch2D.html) \
`circleRect` [Rectangle](../../Murder/Core/Geometry/Rectangle.html) \
`steps` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`drawInfo` [DrawInfo](../../Murder/Core/Graphics/DrawInfo.html) \

#### DrawFilledCircle(Batch2D, Vector2, float, int, T?)
```csharp
public void DrawFilledCircle(Batch2D batch, Vector2 center, float radius, int steps, T? drawInfo)
```
Draws a filled circle centred at `center` with the given `radius`, approximated with `steps` polygon vertices.

**Parameters** \
`batch` [Batch2D](../../Murder/Core/Graphics/Batch2D.html) \
`center` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`radius` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`steps` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`drawInfo` [T?](https://learn.microsoft.com/en-us/dotnet/api/System.Nullable-1?view=net-7.0) \

#### DrawHorizontalLine(Batch2D, int, int, int, Color, float)
```csharp
public void DrawHorizontalLine(Batch2D spriteBatch, int x, int y, int length, Color color, float sorting)
```
Draws a single-pixel horizontal line of `length` pixels starting at `(x, y)`.

**Parameters** \
`spriteBatch` [Batch2D](../../Murder/Core/Graphics/Batch2D.html) \
`x` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`y` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`length` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`color` [Color](../../Murder/Core/Graphics/Color.html) \
`sorting` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### DrawIndexedVertices(Matrix, GraphicsDevice, T[], int, Int16[], int, Effect, BlendState, Texture2D, bool)
```csharp
public void DrawIndexedVertices(Matrix matrix, GraphicsDevice graphicsDevice, T[] vertices, int vertexCount, Int16[] indices, int primitiveCount, Effect effect, BlendState blendState, Texture2D texture, bool smoothing)
```
Submits indexed vertex data directly to the graphics device for custom mesh rendering.

**Parameters** \
`matrix` [Matrix](https://docs.monogame.net/api/Microsoft.Xna.Framework.Matrix.html) \
`graphicsDevice` [GraphicsDevice](https://docs.monogame.net/api/Microsoft.Xna.Framework.Graphics.GraphicsDevice.html) \
`vertices` [T[]](../../) \
`vertexCount` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`indices` [short[]](https://learn.microsoft.com/en-us/dotnet/api/System.Int16?view=net-7.0) \
`primitiveCount` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`effect` [Effect](https://docs.monogame.net/api/Microsoft.Xna.Framework.Graphics.Effect.html) \
`blendState` [BlendState](https://docs.monogame.net/api/Microsoft.Xna.Framework.Graphics.BlendState.html) \
`texture` [Texture2D](https://docs.monogame.net/api/Microsoft.Xna.Framework.Graphics.Texture2D.html) \
`smoothing` [bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### DrawLine(Batch2D, Point, Point, Color, float)
```csharp
public void DrawLine(Batch2D spriteBatch, Point point1, Point point2, Color color, float sort)
```
Draws a line segment between two integer-coordinate points.

**Parameters** \
`spriteBatch` [Batch2D](../../Murder/Core/Graphics/Batch2D.html) \
`point1` [Point](../../Murder/Core/Geometry/Point.html) \
`point2` [Point](../../Murder/Core/Geometry/Point.html) \
`color` [Color](../../Murder/Core/Graphics/Color.html) \
`sort` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### DrawLine(Batch2D, Vector2, float, float, Color, float)
```csharp
public void DrawLine(Batch2D spriteBatch, Vector2 point, float length, float angle, Color color, float sort)
```
Draws a line of `length` pixels starting at `point` and extending in the direction of `angle` (radians).

**Parameters** \
`spriteBatch` [Batch2D](../../Murder/Core/Graphics/Batch2D.html) \
`point` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`length` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`angle` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`color` [Color](../../Murder/Core/Graphics/Color.html) \
`sort` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### DrawLine(Batch2D, Vector2, float, float, Color, float, float)
```csharp
public void DrawLine(Batch2D spriteBatch, Vector2 point, float length, float angle, Color color, float thickness, float sort)
```
Draws a line of `length` pixels at `angle` (radians) with a custom `thickness`.

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
public void DrawLine(Batch2D spriteBatch, Vector2 point1, Vector2 point2, Color color, float sort)
```
Draws a line segment between two float-precision world positions.

**Parameters** \
`spriteBatch` [Batch2D](../../Murder/Core/Graphics/Batch2D.html) \
`point1` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`point2` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`color` [Color](../../Murder/Core/Graphics/Color.html) \
`sort` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### DrawLine(Batch2D, Vector2, Vector2, Color, float, float)
```csharp
public void DrawLine(Batch2D spriteBatch, Vector2 point1, Vector2 point2, Color color, float thickness, float sort)
```
Draws a line segment between two float-precision positions with a custom `thickness`.

**Parameters** \
`spriteBatch` [Batch2D](../../Murder/Core/Graphics/Batch2D.html) \
`point1` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`point2` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`color` [Color](../../Murder/Core/Graphics/Color.html) \
`thickness` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`sort` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### DrawPoint(Batch2D, Point, Color, float)
```csharp
public void DrawPoint(Batch2D spriteBatch, Point pos, Color color, float sorting)
```
Draws a single pixel-sized point at the given coordinates.

**Parameters** \
`spriteBatch` [Batch2D](../../Murder/Core/Graphics/Batch2D.html) \
`pos` [Point](../../Murder/Core/Geometry/Point.html) \
`color` [Color](../../Murder/Core/Graphics/Color.html) \
`sorting` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### DrawPoints(Batch2D, Vector2, Vector2[], Color, float)
```csharp
public void DrawPoints(Batch2D spriteBatch, Vector2 position, Vector2[] points, Color color, float thickness)
```

Draws a list of connecting points

**Parameters** \
`spriteBatch` [Batch2D](../../Murder/Core/Graphics/Batch2D.html) \
\
`position` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
\
`points` [Vector2[]](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
\
`color` [Color](../../Murder/Core/Graphics/Color.html) \
\
`thickness` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
\

#### DrawPoints(Batch2D, Vector2, ReadOnlySpan<T>, Color, float)
```csharp
public void DrawPoints(Batch2D spriteBatch, Vector2 position, ReadOnlySpan<T> points, Color color, float thickness)
```

Draws a list of connecting points

**Parameters** \
`spriteBatch` [Batch2D](../../Murder/Core/Graphics/Batch2D.html) \
\
`position` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
\
`points` [ReadOnlySpan\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.ReadOnlySpan-1?view=net-7.0) \
\
`color` [Color](../../Murder/Core/Graphics/Color.html) \
\
`thickness` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
\

#### DrawPolygon(Batch2D, ImmutableArray<T>, T?)
```csharp
public void DrawPolygon(Batch2D batch, ImmutableArray<T> vertices, T? drawInfo)
```
Draws a closed polygon from the given vertex array using the specified draw parameters.

**Parameters** \
`batch` [Batch2D](../../Murder/Core/Graphics/Batch2D.html) \
`vertices` [ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \
`drawInfo` [T?](https://learn.microsoft.com/en-us/dotnet/api/System.Nullable-1?view=net-7.0) \

#### DrawQuad(Rectangle, Color)
```csharp
public void DrawQuad(Rectangle rect, Color color)
```
Fills the full-screen quad with `color`, ignoring batch sorting; used for full-screen overlays.

**Parameters** \
`rect` [Rectangle](../../Murder/Core/Geometry/Rectangle.html) \
`color` [Color](../../Murder/Core/Graphics/Color.html) \

#### DrawQuadOutline(Rectangle, Color)
```csharp
public void DrawQuadOutline(Rectangle rect, Color color)
```
Draws an outlined quad (border only) over the specified rectangle.

**Parameters** \
`rect` [Rectangle](../../Murder/Core/Geometry/Rectangle.html) \
`color` [Color](../../Murder/Core/Graphics/Color.html) \

#### DrawRectangle(Batch2D, Rectangle, Color, float)
```csharp
public void DrawRectangle(Batch2D batch, Rectangle rectangle, Color color, float sorting)
```
Fills `rectangle` with `color` at the given sort depth.

**Parameters** \
`batch` [Batch2D](../../Murder/Core/Graphics/Batch2D.html) \
`rectangle` [Rectangle](../../Murder/Core/Geometry/Rectangle.html) \
`color` [Color](../../Murder/Core/Graphics/Color.html) \
`sorting` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### DrawRectangleOutline(Batch2D, Rectangle, Color, int, float)
```csharp
public void DrawRectangleOutline(Batch2D spriteBatch, Rectangle rectangle, Color color, int lineWidth, float sorting)
```
Draws the border of `rectangle` with `lineWidth` thickness at `sorting` depth.

**Parameters** \
`spriteBatch` [Batch2D](../../Murder/Core/Graphics/Batch2D.html) \
`rectangle` [Rectangle](../../Murder/Core/Geometry/Rectangle.html) \
`color` [Color](../../Murder/Core/Graphics/Color.html) \
`lineWidth` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`sorting` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### DrawRectangleOutline(Batch2D, Rectangle, Color, int)
```csharp
public void DrawRectangleOutline(Batch2D spriteBatch, Rectangle rectangle, Color color, int lineWidth)
```
Draws the border of `rectangle` with `lineWidth` thickness.

**Parameters** \
`spriteBatch` [Batch2D](../../Murder/Core/Graphics/Batch2D.html) \
`rectangle` [Rectangle](../../Murder/Core/Geometry/Rectangle.html) \
`color` [Color](../../Murder/Core/Graphics/Color.html) \
`lineWidth` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### DrawRectangleOutline(Batch2D, Rectangle, Color)
```csharp
public void DrawRectangleOutline(Batch2D spriteBatch, Rectangle rectangle, Color color)
```
Draws a single-pixel border around `rectangle`.

**Parameters** \
`spriteBatch` [Batch2D](../../Murder/Core/Graphics/Batch2D.html) \
`rectangle` [Rectangle](../../Murder/Core/Geometry/Rectangle.html) \
`color` [Color](../../Murder/Core/Graphics/Color.html) \

#### DrawRepeating(Batch2D, AtlasCoordinates, Rectangle, float)
```csharp
public void DrawRepeating(Batch2D batch, AtlasCoordinates texture, Rectangle area, float sort)
```
Tiles `texture` to fill the entire `area` rectangle.

**Parameters** \
`batch` [Batch2D](../../Murder/Core/Graphics/Batch2D.html) \
`texture` [AtlasCoordinates](../../Murder/Core/Graphics/AtlasCoordinates.html) \
`area` [Rectangle](../../Murder/Core/Geometry/Rectangle.html) \
`sort` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### DrawTexture(Batch2D, Texture2D, Vector2, DrawInfo)
```csharp
public void DrawTexture(Batch2D batch, Texture2D texture, Vector2 position, DrawInfo drawInfo)
```
Draws a raw `Texture2D` (not an atlas sprite) at `position` using the given draw parameters.

**Parameters** \
`batch` [Batch2D](../../Murder/Core/Graphics/Batch2D.html) \
`texture` [Texture2D](https://docs.monogame.net/api/Microsoft.Xna.Framework.Graphics.Texture2D.html) \
`position` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`drawInfo` [DrawInfo](../../Murder/Core/Graphics/DrawInfo.html) \

#### DrawTextureQuad(Texture2D, Rectangle, Rectangle, Matrix, Color, BlendState, Effect, Vector3)
```csharp
public void DrawTextureQuad(Texture2D texture, Rectangle source, Rectangle destination, Matrix matrix, Color color, BlendState blend, Effect shaderEffect, Vector3 colorBlend)
```
Blits `source` region of `texture` into `destination` on screen using the given matrix, color, blend state, shader, and color-blend vector.

**Parameters** \
`texture` [Texture2D](https://docs.monogame.net/api/Microsoft.Xna.Framework.Graphics.Texture2D.html) \
`source` [Rectangle](../../Murder/Core/Geometry/Rectangle.html) \
`destination` [Rectangle](../../Murder/Core/Geometry/Rectangle.html) \
`matrix` [Matrix](https://docs.monogame.net/api/Microsoft.Xna.Framework.Matrix.html) \
`color` [Color](../../Murder/Core/Graphics/Color.html) \
`blend` [BlendState](https://docs.monogame.net/api/Microsoft.Xna.Framework.Graphics.BlendState.html) \
`shaderEffect` [Effect](https://docs.monogame.net/api/Microsoft.Xna.Framework.Graphics.Effect.html) \
`colorBlend` [Vector3](https://docs.monogame.net/api/Microsoft.Xna.Framework.Vector3.html) \

#### DrawTextureQuad(Texture2D, Rectangle, Rectangle, Matrix, Color, BlendState, Effect)
```csharp
public void DrawTextureQuad(Texture2D texture, Rectangle source, Rectangle destination, Matrix matrix, Color color, BlendState blend, Effect shaderEffect)
```
Blits `source` region of `texture` into `destination` using a shader effect and blend state.

**Parameters** \
`texture` [Texture2D](https://docs.monogame.net/api/Microsoft.Xna.Framework.Graphics.Texture2D.html) \
`source` [Rectangle](../../Murder/Core/Geometry/Rectangle.html) \
`destination` [Rectangle](../../Murder/Core/Geometry/Rectangle.html) \
`matrix` [Matrix](https://docs.monogame.net/api/Microsoft.Xna.Framework.Matrix.html) \
`color` [Color](../../Murder/Core/Graphics/Color.html) \
`blend` [BlendState](https://docs.monogame.net/api/Microsoft.Xna.Framework.Graphics.BlendState.html) \
`shaderEffect` [Effect](https://docs.monogame.net/api/Microsoft.Xna.Framework.Graphics.Effect.html) \

#### DrawTextureQuad(Texture2D, Rectangle, Rectangle, Matrix, Color, BlendState)
```csharp
public void DrawTextureQuad(Texture2D texture, Rectangle source, Rectangle destination, Matrix matrix, Color color, BlendState blend)
```
Blits `source` region of `texture` into `destination` with the given blend state.

**Parameters** \
`texture` [Texture2D](https://docs.monogame.net/api/Microsoft.Xna.Framework.Graphics.Texture2D.html) \
`source` [Rectangle](../../Murder/Core/Geometry/Rectangle.html) \
`destination` [Rectangle](../../Murder/Core/Geometry/Rectangle.html) \
`matrix` [Matrix](https://docs.monogame.net/api/Microsoft.Xna.Framework.Matrix.html) \
`color` [Color](../../Murder/Core/Graphics/Color.html) \
`blend` [BlendState](https://docs.monogame.net/api/Microsoft.Xna.Framework.Graphics.BlendState.html) \

#### DrawTextureQuad(Texture2D, Rectangle, Rectangle, Matrix, Color, Effect, BlendState, bool)
```csharp
public void DrawTextureQuad(Texture2D texture, Rectangle source, Rectangle destination, Matrix matrix, Color color, Effect effect, BlendState blend, bool smoothing)
```
Blits `source` region of `texture` into `destination` with smoothing control.

**Parameters** \
`texture` [Texture2D](https://docs.monogame.net/api/Microsoft.Xna.Framework.Graphics.Texture2D.html) \
`source` [Rectangle](../../Murder/Core/Geometry/Rectangle.html) \
`destination` [Rectangle](../../Murder/Core/Geometry/Rectangle.html) \
`matrix` [Matrix](https://docs.monogame.net/api/Microsoft.Xna.Framework.Matrix.html) \
`color` [Color](../../Murder/Core/Graphics/Color.html) \
`effect` [Effect](https://docs.monogame.net/api/Microsoft.Xna.Framework.Graphics.Effect.html) \
`blend` [BlendState](https://docs.monogame.net/api/Microsoft.Xna.Framework.Graphics.BlendState.html) \
`smoothing` [bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### DrawVerticalLine(Batch2D, int, int, int, Color, float)
```csharp
public void DrawVerticalLine(Batch2D spriteBatch, int x, int y, int length, Color color, float sorting)
```
Draws a single-pixel vertical line of `length` pixels starting at `(x, y)`.

**Parameters** \
`spriteBatch` [Batch2D](../../Murder/Core/Graphics/Batch2D.html) \
`x` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`y` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`length` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`color` [Color](../../Murder/Core/Graphics/Color.html) \
`sorting` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### MessageCompleteAnimations(Entity, SpriteComponent)
```csharp
public void MessageCompleteAnimations(Entity e, SpriteComponent s)
```
Sends an `AnimationCompleteMessage` for all completed animations on entity `e` given sprite component `s`.

**Parameters** \
`e` [Entity](../../Bang/Entities/Entity.html) \
`s` [SpriteComponent](../../Murder/Components/SpriteComponent.html) \

#### MessageCompleteAnimations(Entity)
```csharp
public void MessageCompleteAnimations(Entity e)
```
Sends animation-complete messages for all finished animations on entity `e`, reading its current sprite component.

**Parameters** \
`e` [Entity](../../Bang/Entities/Entity.html) \

#### TriggerEventsIfNeeded(Entity, RenderedSpriteCacheComponent, bool)
```csharp
public void TriggerEventsIfNeeded(Entity e, RenderedSpriteCacheComponent cache, bool useUnscaledTime)
```
Fires any animation frame events that occurred since the last render for entity `e`.

**Parameters** \
`e` [Entity](../../Bang/Entities/Entity.html) \
`cache` [RenderedSpriteCacheComponent](../../Murder/Components/Graphics/RenderedSpriteCacheComponent.html) \
`useUnscaledTime` [bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### TriggerEventsIfNeeded(Entity, RenderedSpriteCacheComponent, float, float)
```csharp
public void TriggerEventsIfNeeded(Entity e, RenderedSpriteCacheComponent cache, float previousTime, float currentTime)
```
Fires any animation frame events that fell within the time window `[previousTime, currentTime]` for entity `e`.

**Parameters** \
`e` [Entity](../../Bang/Entities/Entity.html) \
`cache` [RenderedSpriteCacheComponent](../../Murder/Components/Graphics/RenderedSpriteCacheComponent.html) \
`previousTime` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`currentTime` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \



⚡