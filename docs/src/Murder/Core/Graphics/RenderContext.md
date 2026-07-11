# RenderContext

**Namespace:** Murder.Core.Graphics \
**Assembly:** Murder.dll

```csharp
public class RenderContext : IDisposable
```

Manages all `Batch2D` layers, render targets, and the active camera for one complete rendering frame.

**Intent:** Serves as the central hub for all drawing activity — it owns every sprite batch, the camera, and the pipeline of render targets from game-resolution through to the final screen buffer.

**Use-case:** Receive a `RenderContext` in your `IMurderRenderSystem.Draw()` call and use batch properties such as `GameplayBatch` or `UiBatch` to issue sprite draw calls; override `RenderContext` in your game assembly to add custom render passes.

**Implements:** _[IDisposable](https://learn.microsoft.com/en-us/dotnet/api/System.IDisposable?view=net-7.0)_

### ⭐ Constructors
```csharp
public RenderContext(GraphicsDevice graphicsDevice, Camera2D camera, RenderContextFlags settings)
```

A context for how to render your game. Holds everything you need to draw on the screen.
            To make your own, extend this class and add it to [Game.CreateRenderContext(Microsoft.Xna.Framework.Graphics.GraphicsDevice,Murder.Core.Graphics.Camera2D,Murder.Core.Graphics.RenderContextFlags)](../../../Murder/Game.html#createrendercontext(graphicsdevice,)
            Extending your [Batches2D](../../../Murder/Core/Graphics/Batches2D.html) file is also recommended.

**Parameters** \
`graphicsDevice` [GraphicsDevice](https://docs.monogame.net/api/Microsoft.Xna.Framework.Graphics.GraphicsDevice.html) \
`camera` [Camera2D](../../../Murder/Core/Graphics/Camera2D.html) \
`settings` [RenderContextFlags](../../../Murder/Core/Graphics/RenderContextFlags.html) \

### ⭐ Properties
#### _debugTarget
```csharp
protected RenderTarget2D _debugTarget;
```

Internal render target used to accumulate debug overlay draws.

**Returns** \
[RenderTarget2D](https://docs.monogame.net/api/Microsoft.Xna.Framework.Graphics.RenderTarget2D.html) \
#### _debugTargetPreview
```csharp
protected RenderTarget2D _debugTargetPreview;
```

Internal render target used to capture a snapshot of one batch step when previewing individual render passes in the editor.

**Returns** \
[RenderTarget2D](https://docs.monogame.net/api/Microsoft.Xna.Framework.Graphics.RenderTarget2D.html) \
#### _finalTarget
```csharp
protected RenderTarget2D _finalTarget;
```

The final screen target, has the real screen size.

**Returns** \
[RenderTarget2D](https://docs.monogame.net/api/Microsoft.Xna.Framework.Graphics.RenderTarget2D.html) \
#### _floorBufferTarget
```csharp
protected RenderTarget2D _floorBufferTarget;
```

Render target for the floor layer drawn behind the gameplay batch.

**Returns** \
[RenderTarget2D](https://docs.monogame.net/api/Microsoft.Xna.Framework.Graphics.RenderTarget2D.html) \
#### _graphicsDevice
```csharp
protected GraphicsDevice _graphicsDevice;
```

The underlying MonoGame `GraphicsDevice` used to create render targets and issue draw calls.

**Returns** \
[GraphicsDevice](https://docs.monogame.net/api/Microsoft.Xna.Framework.Graphics.GraphicsDevice.html) \
#### _mainTarget
```csharp
protected RenderTarget2D _mainTarget;
```

Primary game-resolution render target where all gameplay and floor sprites are composited before post-processing.

**Returns** \
[RenderTarget2D](https://docs.monogame.net/api/Microsoft.Xna.Framework.Graphics.RenderTarget2D.html) \
#### _spriteBatches
```csharp
public Batch2D[] _spriteBatches;
```

Array of all registered `Batch2D` instances, indexed by their batch ID constants defined in `Batches2D`.

**Returns** \
[Batch2D[]](../../../Murder/Core/Graphics/Batch2D.html) \
#### _subPixelOffset
```csharp
protected Vector2 _subPixelOffset;
```

Sub-pixel camera offset applied to prevent texture bleeding at fractional camera positions.

**Returns** \
[Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
#### _tempTarget
```csharp
protected RenderTarget2D _tempTarget;
```

Temporary buffer with the camera size. Used so we can apply effects
            such as limited palette and bloom on a smaller screen before applying
            it to the final target

**Returns** \
[RenderTarget2D](https://docs.monogame.net/api/Microsoft.Xna.Framework.Graphics.RenderTarget2D.html) \
#### _uiTarget
```csharp
protected RenderTarget2D _uiTarget;
```

Render target that receives all UI sprites drawn above the gameplay layer.

**Returns** \
[RenderTarget2D](https://docs.monogame.net/api/Microsoft.Xna.Framework.Graphics.RenderTarget2D.html) \
#### _useDebugBatches
```csharp
protected readonly bool _useDebugBatches;
```

Whether debug batches (`DebugBatch`, `DebugFxBatch`) were enabled when this context was created via `RenderContextFlags.Debug`.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
#### BackColor
```csharp
public Color BackColor { get; }
```

Background clear color read from the active game profile, applied before every frame.

**Returns** \
[Color](../../../Murder/Core/Graphics/Color.html) \
#### CachedTextTextures
```csharp
public readonly CacheDictionary<TKey, TValue> CachedTextTextures;
```

Per-string texture cache used to avoid re-rendering static text every frame; holds up to 32 recently used text textures.

**Returns** \
[CacheDictionary\<TKey, TValue\>](../../../Murder/Utilities/CacheDictionary-2.html) \
#### Camera
```csharp
public readonly Camera2D Camera;
```

The active camera used for rendering scenes.

**Returns** \
[Camera2D](../../../Murder/Core/Graphics/Camera2D.html) \
#### CAMERA_BLEED
```csharp
public readonly static int CAMERA_BLEED;
```

Extra pixel margin added to each camera edge to hide seam artifacts at viewport boundaries.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
#### CAMERA_BLEED_VECTOR
```csharp
public readonly static Vector2 CAMERA_BLEED_VECTOR;
```

`CAMERA_BLEED` expressed as a `Vector2` for convenient use in offset calculations.

**Returns** \
[Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
#### ColorGrade
```csharp
public Texture2D ColorGrade;
```

Optional color-grading lookup table texture applied as a post-processing step; null if color grading is disabled.

**Returns** \
[Texture2D](https://docs.monogame.net/api/Microsoft.Xna.Framework.Graphics.Texture2D.html) \
#### DebugBatch
```csharp
public Batch2D DebugBatch { get; }
```

Only used if [RenderContextFlags.Debug](../../../Murder/Core/Graphics/RenderContextFlags.html#debug) is set. Influenced by the camera.

**Returns** \
[Batch2D](../../../Murder/Core/Graphics/Batch2D.html) \
#### DebugFxBatch
```csharp
public Batch2D DebugFxBatch { get; }
```

Only used if [RenderContextFlags.Debug](../../../Murder/Core/Graphics/RenderContextFlags.html#debug) is set, has a nice effect to it. Influenced by the camera.

**Returns** \
[Batch2D](../../../Murder/Core/Graphics/Batch2D.html) \
#### FloorBatch
```csharp
public Batch2D FloorBatch { get; }
```

Renders behind the [RenderContext.GameplayBatch](../../../Murder/Core/Graphics/RenderContext.html#gameplaybatch), influenced by the camera.

**Returns** \
[Batch2D](../../../Murder/Core/Graphics/Batch2D.html) \
#### GameBufferSize
```csharp
public Point GameBufferSize;
```

Pixel dimensions of the game-resolution render buffer (independent of the window size).

**Returns** \
[Point](../../../Murder/Core/Geometry/Point.html) \
#### GameplayBatch
```csharp
public Batch2D GameplayBatch { get; }
```

Intended to be the main gameplay batch, influenced by the camera.

**Returns** \
[Batch2D](../../../Murder/Core/Graphics/Batch2D.html) \
#### GameUiBatch
```csharp
public Batch2D GameUiBatch { get; }
```

Renders in front of the [RenderContext.GameplayBatch](../../../Murder/Core/Graphics/RenderContext.html#gameplaybatch), influenced by the camera.

**Returns** \
[Batch2D](../../../Murder/Core/Graphics/Batch2D.html) \
#### LastRenderTarget
```csharp
public RenderTarget2D LastRenderTarget { get; }
```

The screen-resolution render target produced at the end of the previous frame.

**Returns** \
[RenderTarget2D](https://docs.monogame.net/api/Microsoft.Xna.Framework.Graphics.RenderTarget2D.html) \
#### MainTarget
```csharp
public RenderTarget2D MainTarget { get; }
```

The game-resolution render target for the current frame.

**Returns** \
[RenderTarget2D](https://docs.monogame.net/api/Microsoft.Xna.Framework.Graphics.RenderTarget2D.html) \
#### PreviewState
```csharp
public BatchPreviewState PreviewState;
```

Controls which intermediate render pass is displayed when stepping through batch previews in the editor.

**Returns** \
[BatchPreviewState](../../../Murder/Core/Graphics/BatchPreviewState.html) \
#### PreviewStretch
```csharp
public bool PreviewStretch;
```

When true, the preview render target is stretched to fill the full screen in the editor preview.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
#### RenderToScreen
```csharp
public bool RenderToScreen;
```

When false, the final render target is not blitted to the display; useful for off-screen rendering or screenshots.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
#### Settings
```csharp
protected readonly RenderContextFlags Settings;
```

The `RenderContextFlags` bitmask that was passed when this context was constructed, controlling optional features such as debug batches and custom shaders.

**Returns** \
[RenderContextFlags](../../../Murder/Core/Graphics/RenderContextFlags.html) \
#### SubPixelOffset
```csharp
public Vector2 SubPixelOffset { get; }
```

Sub-pixel camera alignment offset exposed to render systems for precise pixel-perfect positioning.

**Returns** \
[Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
#### UiBatch
```csharp
public Batch2D UiBatch { get; }
```

Renders above everything, ignores any camera movement.

**Returns** \
[Batch2D](../../../Murder/Core/Graphics/Batch2D.html) \
#### Viewport
```csharp
public Viewport Viewport;
```

The active screen viewport region that the game image is rendered into.

**Returns** \
[Viewport](../../../Murder/Core/Viewport.html) \
### ⭐ Methods
#### SetupRenderTarget(RenderTarget2D, int, int, Color, bool)
```csharp
protected RenderTarget2D SetupRenderTarget(RenderTarget2D existingTarget, int width, int height, Color clearColor, bool preserveContents)
```

Sets up a new RenderTarget2D, disposing of the existing one if necessary.

**Parameters** \
`existingTarget` [RenderTarget2D](https://docs.monogame.net/api/Microsoft.Xna.Framework.Graphics.RenderTarget2D.html) \
\
`width` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
\
`height` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
\
`clearColor` [Color](../../../Murder/Core/Graphics/Color.html) \
\
`preserveContents` [bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
\

**Returns** \
[RenderTarget2D](https://docs.monogame.net/api/Microsoft.Xna.Framework.Graphics.RenderTarget2D.html) \
\

#### AfterMainRender(RenderTarget2D)
```csharp
protected virtual void AfterMainRender(RenderTarget2D mainTarget)
```

Called right after [RenderContext.GameUiBatch](../../../Murder/Core/Graphics/RenderContext.html#gameuibatch) end.

**Parameters** \
`mainTarget` [RenderTarget2D](https://docs.monogame.net/api/Microsoft.Xna.Framework.Graphics.RenderTarget2D.html) \
\

#### AfterUiRender(RenderTarget2D)
```csharp
protected virtual void AfterUiRender(RenderTarget2D uiTarget)
```

Called right after the [RenderContext.UiBatch](../../../Murder/Core/Graphics/RenderContext.html#uibatch) ends.

**Parameters** \
`uiTarget` [RenderTarget2D](https://docs.monogame.net/api/Microsoft.Xna.Framework.Graphics.RenderTarget2D.html) \
\

#### BeforeScreenRender(RenderTarget2D)
```csharp
protected virtual void BeforeScreenRender(RenderTarget2D finalTarget)
```

Last chance to render anything before the contents are drawn on the screen!

**Parameters** \
`finalTarget` [RenderTarget2D](https://docs.monogame.net/api/Microsoft.Xna.Framework.Graphics.RenderTarget2D.html) \
\

#### UnloadImpl()
```csharp
protected virtual void UnloadImpl()
```

Override for custom unload implementations in derived classes.

#### RegisterSpriteBatch(int, Batch2D)
```csharp
protected void RegisterSpriteBatch(int index, Batch2D batch)
```

Registers a SpriteBatch at a specified index. If the index is already taken, it will be overwritten.

**Parameters** \
`index` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
\
`batch` [Batch2D](../../../Murder/Core/Graphics/Batch2D.html) \
\

#### TakeScreenshotIfNecessary(RenderTarget2D)
```csharp
protected void TakeScreenshotIfNecessary(RenderTarget2D target)
```

Saves the provided render target to disk if a screenshot was requested via `SaveScreenShot()`.

**Parameters** \
`target` [RenderTarget2D](https://docs.monogame.net/api/Microsoft.Xna.Framework.Graphics.RenderTarget2D.html) \

#### GetBatch(int)
```csharp
public Batch2D GetBatch(int index)
```

Returns the `Batch2D` registered at the given index, or logs an error and returns batch 0 if the index is invalid.

**Parameters** \
`index` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

**Returns** \
[Batch2D](../../../Murder/Core/Graphics/Batch2D.html) \

#### RefreshWindow(GraphicsDevice, Point, Point, ViewportResizeStyle)
```csharp
public bool RefreshWindow(GraphicsDevice graphicsDevice, Point viewportSize, Point nativeResolution, ViewportResizeStyle viewportResizeMode)
```

Refreshes the window with the new viewport size and camera scale.

**Parameters** \
`graphicsDevice` [GraphicsDevice](https://docs.monogame.net/api/Microsoft.Xna.Framework.Graphics.GraphicsDevice.html) \
`viewportSize` [Point](../../../Murder/Core/Geometry/Point.html) \
`nativeResolution` [Point](../../../Murder/Core/Geometry/Point.html) \
`viewportResizeMode` [ViewportResizeStyle](../../../Murder/Core/Graphics/ViewportResizeStyle.html) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
\

#### GetRenderTargetFromEnum(RenderTargets)
```csharp
public virtual Texture2D GetRenderTargetFromEnum(RenderTargets inspectingRenderTarget)
```

Resolves a `RenderTargets` enum value to its underlying `Texture2D` render target.

**Parameters** \
`inspectingRenderTarget` [RenderTargets](../../../Murder/Core/Graphics/RenderTargets.html) \

**Returns** \
[Texture2D](https://docs.monogame.net/api/Microsoft.Xna.Framework.Graphics.Texture2D.html) \

#### Begin()
```csharp
public virtual void Begin()
```

Begins all registered sprite batches in preparation for drawing the current frame.

#### Dispose()
```csharp
public virtual void Dispose()
```

Disposes of all associated resources.

#### End()
```csharp
public virtual void End()
```

Flushes all active sprite batches and ends the current frame.

#### Initialize()
```csharp
public virtual void Initialize()
```

Allocates render targets, creates all default sprite batches, and performs initial viewport setup.

#### UpdateViewport()
```csharp
public virtual void UpdateViewport()
```

Recomputes the viewport dimensions and camera scale factor after a window resize event.

#### CreateDebugPreviewIfNecessary(BatchPreviewState, RenderTarget2D)
```csharp
public void CreateDebugPreviewIfNecessary(BatchPreviewState currentState, RenderTarget2D target)
```

Copies `target` into the debug preview buffer when `currentState` matches the active `PreviewState`, enabling step-by-step batch inspection.

**Parameters** \
`currentState` [BatchPreviewState](../../../Murder/Core/Graphics/BatchPreviewState.html) \
`target` [RenderTarget2D](https://docs.monogame.net/api/Microsoft.Xna.Framework.Graphics.RenderTarget2D.html) \

#### SaveScreenShot(Rectangle)
```csharp
public void SaveScreenShot(Rectangle cameraRect)
```

Saves a screenshot of the specified camera area.

**Parameters** \
`cameraRect` [Rectangle](../../../Murder/Core/Geometry/Rectangle.html) \
\

#### Unload()
```csharp
public void Unload()
```

Unload the render context.
            Called when the render context is no longer being actively displayed.



⚡