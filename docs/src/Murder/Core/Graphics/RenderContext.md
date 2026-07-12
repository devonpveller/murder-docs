# RenderContext

**Namespace:** Murder.Core.Graphics \
**Assembly:** Murder.dll

```csharp
public class RenderContext : IDisposable
```

Manages all `Batch2D` layers, render targets, and the active camera for one complete rendering frame.

**Intent:** Serves as the central hub for all drawing activity — it owns every sprite batch, the camera, and the pipeline of render targets from game-resolution through to the final screen buffer, and drives the sequence of `Begin()`/system draws/`End()` that turns queued sprite batches into a composited frame on screen.

**Use-case:** Receive a `RenderContext` in your `IMurderRenderSystem.Draw()` call and use batch properties such as `GameplayBatch` or `UiBatch` to issue sprite draw calls; override `RenderContext` in your game assembly (registering it via `Game.CreateRenderContext`) to add custom render passes, targets, or post-processing, extending the `AfterMainRender`/`AfterUiRender`/`BeforeScreenRender` hooks rather than reimplementing `End()`.

**Implements:** _[IDisposable](https://learn.microsoft.com/en-us/dotnet/api/System.IDisposable?view=net-7.0)_

### ⭐ Constructors

```csharp
public RenderContext(GraphicsDevice graphicsDevice, Camera2D camera, RenderContextFlags settings)
```

A context for how to render your game. Holds everything you need to draw on the screen.
To make your own, extend this class and add it to [Game.CreateRenderContext(Microsoft.Xna.Framework.Graphics.GraphicsDevice,Murder.Core.Graphics.Camera2D,Murder.Core.Graphics.RenderContextFlags)](../../../Murder/Game.html#createrendercontext(graphicsdevice,)
Extending your [Batches2D](../../../Murder/Core/Graphics/Batches2D.html) file is also recommended.
Stores `settings` and derives `_useDebugBatches` from `RenderContextFlags.Debug`, then immediately calls `Initialize()` to register the default batches and perform the first viewport setup.

**Parameters** \
`graphicsDevice` [GraphicsDevice](https://docs.monogame.net/api/Microsoft.Xna.Framework.Graphics.GraphicsDevice.html) \
`camera` [Camera2D](../../../Murder/Core/Graphics/Camera2D.html) \
`settings` [RenderContextFlags](../../../Murder/Core/Graphics/RenderContextFlags.html) \

### ⭐ Properties

#### \_debugTarget

```csharp
protected RenderTarget2D _debugTarget;
```

Render target that debug batches (`DebugFxBatch`, `DebugBatch`) are drawn into when `RenderContextFlags.Debug` is set; composited on top of the final frame at the end of `End()`.

**Returns** \
[RenderTarget2D](https://docs.monogame.net/api/Microsoft.Xna.Framework.Graphics.RenderTarget2D.html) \

#### \_debugTargetPreview

```csharp
protected RenderTarget2D _debugTargetPreview;
```

Snapshot buffer, matching the size of whatever target was last captured, used to display a step-by-step batch preview in the editor. Only allocated on demand by `CreateDebugPreviewIfNecessary`.

**Returns** \
[RenderTarget2D](https://docs.monogame.net/api/Microsoft.Xna.Framework.Graphics.RenderTarget2D.html) \

#### \_finalTarget

```csharp
protected RenderTarget2D _finalTarget;
```

The final screen target, has the real screen size.

**Returns** \
[RenderTarget2D](https://docs.monogame.net/api/Microsoft.Xna.Framework.Graphics.RenderTarget2D.html) \

#### \_floorBufferTarget

```csharp
protected RenderTarget2D _floorBufferTarget;
```

Reserved render target for a dedicated floor buffer. Currently declared and disposed alongside the other targets but never actually allocated by the base `RenderContext` (always `null` here); kept available for derived classes that want to render the floor layer to its own target instead of sharing `FloorBatch`'s pass over `_mainTarget`.

**Returns** \
[RenderTarget2D](https://docs.monogame.net/api/Microsoft.Xna.Framework.Graphics.RenderTarget2D.html) \

#### \_graphicsDevice

```csharp
protected GraphicsDevice _graphicsDevice;
```

The underlying MonoGame/FNA `GraphicsDevice` used to create render targets and issue draw calls.

**Returns** \
[GraphicsDevice](https://docs.monogame.net/api/Microsoft.Xna.Framework.Graphics.GraphicsDevice.html) \

#### \_mainTarget

```csharp
protected RenderTarget2D _mainTarget;
```

Primary game-resolution render target where floor and gameplay sprites are composited before post-processing and UI compositing.

**Returns** \
[RenderTarget2D](https://docs.monogame.net/api/Microsoft.Xna.Framework.Graphics.RenderTarget2D.html) \

#### \_spriteBatches

```csharp
public Batch2D[] _spriteBatches;
```

All registered `Batch2D` instances, indexed by the batch ID constants defined in `Batches2D` (e.g. `Batches2D.GameplayBatchId`). Populated via `RegisterSpriteBatch`; prefer the named properties (`GameplayBatch`, `UiBatch`, etc.) or `GetBatch` over indexing this array directly.

**Returns** \
[Batch2D[]](../../../Murder/Core/Graphics/Batch2D.html) \

#### \_subPixelOffset

```csharp
protected Vector2 _subPixelOffset;
```

Sub-pixel remainder of the camera's world position, used to offset the final composite draw so that fractional camera movement doesn't cause visible texture-edge bleeding/jitter at the game's native resolution. Recomputed every `End()`.

**Returns** \
[Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

#### \_tempTarget

```csharp
protected RenderTarget2D _tempTarget;
```

Temporary buffer with the camera size. Used so we can apply effects
such as limited palette and bloom on a smaller screen before applying
it to the final target

**Returns** \
[RenderTarget2D](https://docs.monogame.net/api/Microsoft.Xna.Framework.Graphics.RenderTarget2D.html) \

#### \_uiTarget

```csharp
protected RenderTarget2D _uiTarget;
```

Render target, sized to the camera viewport, that receives all UI sprites drawn above the gameplay layer (`UiBatch`).

**Returns** \
[RenderTarget2D](https://docs.monogame.net/api/Microsoft.Xna.Framework.Graphics.RenderTarget2D.html) \

#### \_useDebugBatches

```csharp
protected readonly bool _useDebugBatches;
```

Whether debug batches (`DebugBatch`, `DebugFxBatch`) and their render target were allocated for this context, per the `RenderContextFlags.Debug` flag passed to the constructor.

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

Per-string texture cache used to avoid re-rendering static text every frame; holds up to 32 recently used text textures, evicting the least-recently-used entry beyond that.

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

Extra pixel margin added around the camera's visible area on `_mainTarget`/`_tempTarget`, so post-processing/pixel-snapping doesn't sample past the edge and cause seam artifacts.

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

Optional color-grading lookup table texture; not applied by the base `RenderContext` itself but available for derived classes to sample during their own post-processing pass. Null unless a derived class assigns it.

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

#### DoNotRender

```csharp
public bool DoNotRender;
```

When true, `Begin`/`End` still run their bookkeeping (viewport refresh, camera lock/unlock) but `End` skips flushing/compositing any batches, so nothing is drawn to the render targets or screen this frame. Useful for pausing presentation without pausing the render pipeline's state tracking, e.g. while a loading screen owns the screen.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

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

Pixel dimensions of the game-resolution render buffer (`_mainTarget`/`_tempTarget`), independent of the actual window size. Recomputed by `UpdateViewport`.

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

The screen-resolution render target produced at the end of the previous completed frame — what actually got (or would get) blitted to the display.

**Returns** \
[RenderTarget2D](https://docs.monogame.net/api/Microsoft.Xna.Framework.Graphics.RenderTarget2D.html) \

#### MainTarget

```csharp
public RenderTarget2D MainTarget { get; }
```

The game-resolution render target for the current frame; `null` until `UpdateViewport` has run at least once.

**Returns** \
[RenderTarget2D](https://docs.monogame.net/api/Microsoft.Xna.Framework.Graphics.RenderTarget2D.html) \

#### PreviewState

```csharp
public BatchPreviewState PreviewState;
```

Which intermediate render pass, if any, to copy into the debug preview buffer this frame via `CreateDebugPreviewIfNecessary`; set this to step through individual batches/targets while debugging.

**Returns** \
[BatchPreviewState](../../../Murder/Core/Graphics/BatchPreviewState.html) \

#### PreviewStretch

```csharp
public bool PreviewStretch;
```

When true and a debug preview is active, the preview render target is stretched to fill the full screen instead of drawn at its native size.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### RenderToScreen

```csharp
public bool RenderToScreen;
```

When false, `End` still composites and flushes all batches but skips the final blit to the display; useful for off-screen rendering, screenshot pipelines, or headless rendering.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### ScreenFade

```csharp
public float ScreenFade;
```

Not used by the base `RenderContext`, but can be used by derived classes (e.g. to drive a full-screen fade-to-black/white overlay in their own post-processing hook).

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### Settings

```csharp
protected readonly RenderContextFlags Settings;
```

The `RenderContextFlags` bitmask that was passed when this context was constructed, controlling optional features such as debug batches and editor-hosted viewport scaling.

**Returns** \
[RenderContextFlags](../../../Murder/Core/Graphics/RenderContextFlags.html) \

#### SubPixelOffset

```csharp
public Vector2 SubPixelOffset { get; }
```

Sub-pixel camera alignment offset, recomputed every `End()`, exposed so render systems can nudge their own draws (e.g. debug overlays) to line up with the pixel-snapped camera without texture bleeding.

**Returns** \
[Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

#### TakingScreenshot

```csharp
public bool TakingScreenshot { get; }
```

Whether a gameplay screenshot has been requested via `SaveGameplayScreenshot` and is still pending capture.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

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

The active screen viewport region (window size, native resolution, and scale) that the game image is rendered into.

**Returns** \
[Viewport](../../../Murder/Core/Viewport.html) \

### ⭐ Methods

#### AfterMainRender(RenderTarget2D)

```csharp
protected virtual void AfterMainRender(RenderTarget2D mainTarget)
```

Called right after [RenderContext.FloorBatch](../../../Murder/Core/Graphics/RenderContext.html#floorbatch), [RenderContext.GameplayBatch](../../../Murder/Core/Graphics/RenderContext.html#gameplaybatch) and [RenderContext.GameUiBatch](../../../Murder/Core/Graphics/RenderContext.html#gameuibatch) end.

**Parameters** \
`mainTarget` [RenderTarget2D](https://docs.monogame.net/api/Microsoft.Xna.Framework.Graphics.RenderTarget2D.html) \

#### AfterUiRender(RenderTarget2D)

```csharp
protected virtual void AfterUiRender(RenderTarget2D uiTarget)
```

Called right after the [RenderContext.UiBatch](../../../Murder/Core/Graphics/RenderContext.html#uibatch) ends.

**Parameters** \
`uiTarget` [RenderTarget2D](https://docs.monogame.net/api/Microsoft.Xna.Framework.Graphics.RenderTarget2D.html) \

#### Begin()

```csharp
public virtual void Begin()
```

Starts a new render frame: applies any pending window-size change (via `RefreshWindow`), (re)computes the viewport on the first call or after a resize (via `UpdateViewport`), locks the `Camera` against further changes for the duration of the frame, and calls `Batch2D.Begin()` on every registered batch. Call once per frame, paired with a matching `End()`; skips the batch-begin step entirely when `DoNotRender` is set.

#### BeforeScreenRender(RenderTarget2D)

```csharp
protected virtual void BeforeScreenRender(RenderTarget2D finalTarget)
```

Last chance to render anything before the contents are drawn on the screen!

**Parameters** \
`finalTarget` [RenderTarget2D](https://docs.monogame.net/api/Microsoft.Xna.Framework.Graphics.RenderTarget2D.html) \

#### CreateDebugPreviewIfNecessary(BatchPreviewState, RenderTarget2D)

```csharp
public void CreateDebugPreviewIfNecessary(BatchPreviewState currentState, RenderTarget2D target)
```

If `currentState` matches the currently selected `PreviewState`, copies `target` into the debug preview buffer so it can be shown instead of the final composited frame — this is how the editor's step-by-step batch preview works. Compiled out entirely in non-DEBUG builds via a `[Conditional("DEBUG")]` attribute, so it is safe (and a no-op) to call from release code paths.

**Parameters** \
`currentState` [BatchPreviewState](../../../Murder/Core/Graphics/BatchPreviewState.html) \
`target` [RenderTarget2D](https://docs.monogame.net/api/Microsoft.Xna.Framework.Graphics.RenderTarget2D.html) \

#### Dispose()

```csharp
public virtual void Dispose()
```

Disposes of all associated resources: `CachedTextTextures` and every allocated render target (`_floorBufferTarget`, `_uiTarget`, `_mainTarget`, `_debugTarget`, `_tempTarget`, `_finalTarget`).

#### End()

```csharp
public virtual void End()
```

Finishes the current render frame: ends every registered batch in dependency order (floor → gameplay → game-UI → UI → debug), composites them together through `_tempTarget`/`_mainTarget`/`_uiTarget` into `_finalTarget` using the game's pixel shader, takes any pending screenshot, invokes the `AfterMainRender`/`AfterUiRender`/`BeforeScreenRender` extension points along the way, and finally blits the result to the screen (unless `RenderToScreen` is false). Must be paired with a preceding `Begin()` call; unlocks the `Camera` when done. When `DoNotRender` is set, only unlocks the camera and returns immediately without touching any batches or targets.

#### GetBatch(int)

```csharp
public Batch2D GetBatch(int index)
```

Returns the `Batch2D` registered at the given index (see the constants in `Batches2D`), or logs an error and returns batch 0 if the index is invalid, so a bad batch ID degrades gracefully instead of crashing rendering.

**Parameters** \
`index` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

**Returns** \
[Batch2D](../../../Murder/Core/Graphics/Batch2D.html) \

#### GetRenderTargetFromEnum(RenderTargets)

```csharp
public virtual Texture2D GetRenderTargetFromEnum(RenderTargets inspectingRenderTarget)
```

Resolves a `RenderTargets` enum value to its underlying `Texture2D` render target, so editor tooling (or any code that only has an enum identifier, e.g. from a dropdown) can inspect an arbitrary base render target by name instead of poking at the protected fields directly. Throws if the resolved target hasn't been allocated yet.

**Parameters** \
`inspectingRenderTarget` [RenderTargets](../../../Murder/Core/Graphics/RenderTargets.html) \

**Returns** \
[Texture2D](https://docs.monogame.net/api/Microsoft.Xna.Framework.Graphics.Texture2D.html) \

#### Initialize()

```csharp
public virtual void Initialize()
```

One-time setup: registers the default sprite batches (gameplay, floor, game-UI, UI, and — when `RenderContextFlags.Debug` is set — the debug batches), then performs the initial viewport setup. Called automatically from the constructor; calling it again after the first time logs a warning and does nothing. Override to register additional custom batches via `RegisterSpriteBatch`, calling `base.Initialize()` first.

#### OnClientWindowChanged(WindowChangeSettings)

```csharp
public virtual bool OnClientWindowChanged(WindowChangeSettings settings)
```

Notifies this context that the client window size (or native resolution) changed. If the new settings actually differ from the current `Viewport` (or `settings.Force` is set), stores them as pending so the next `Begin()` picks them up via `RefreshWindow`; otherwise does nothing. Called by the engine's window-resize handling.

**Parameters** \
`settings` [WindowChangeSettings](../../../Murder/Core/Graphics/WindowChangeSettings.html) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### OnShadersReloaded()

```csharp
public virtual void OnShadersReloaded()
```

Called after the game's shaders have been hot-reloaded (e.g. by the editor's shader-watcher), so a derived render context can re-fetch shader references or reset any cached technique/parameter state that pointed at the now-replaced shader instances. No-op in the base `RenderContext`.

#### OnViewportChanged()

```csharp
public virtual void OnViewportChanged()
```

Marks the viewport as dirty so `Begin()` calls `UpdateViewport()` again before the next frame, reallocating all render targets at their (possibly new) size. Call this after changing anything that affects the camera's pixel dimensions outside of the normal window-resize flow.

#### RefreshWindow()

```csharp
protected bool RefreshWindow()
```

Applies a pending window-size change queued by `OnClientWindowChanged`, if any: recomputes `Viewport` from the pending size/native-resolution/scaling request (forcing `ScalingKind.ThreeX` when `RenderContextFlags.Editor` is set, regardless of the player's scaling preference), resizes the `Camera` to match, and marks the viewport dirty so the next `Begin()` reallocates render targets via `UpdateViewport`. Called from `Begin()` and from `Initialize()`; does nothing (and returns `false`) if there is no pending change.

**Returns** \
Whether the window actually required a refresh. \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### RegisterSpriteBatch(int, Batch2D)

```csharp
protected void RegisterSpriteBatch(int index, Batch2D batch)
```

Registers a SpriteBatch at a specified index. If the index is already taken, it will be overwritten (a warning is logged when that happens, since it's rarely intentional). The `_spriteBatches` array is grown automatically if `index` is out of its current bounds.

**Remarks** \
This will automatically trigger a `Batch2D.Begin(Matrix)` call on `Begin`, but will not trigger a `Batch2D.End()`. For now you need to extend `End()` and include it yourself.

**Parameters** \
`index` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`batch` [Batch2D](../../../Murder/Core/Graphics/Batch2D.html) \

#### SaveGameplayScreenshot()

```csharp
public void SaveGameplayScreenshot()
```

Requests that the next couple of frames' gameplay buffer be captured and saved to disk as a PNG (tracked via `TakingScreenshot`). Waits a couple of frames rather than capturing immediately so the request can be issued from, e.g., a key-press handler without capturing mid-frame UI such as the prompt that triggered it.

#### SaveScreenshot(RenderTarget2D, Point)

```csharp
protected void SaveScreenshot(RenderTarget2D screenshot, Point size)
```

Encodes `screenshot` as a PNG and writes it to the game's screenshot folder with a timestamped file name.

**Parameters** \
`screenshot` [RenderTarget2D](https://docs.monogame.net/api/Microsoft.Xna.Framework.Graphics.RenderTarget2D.html) \
`size` [Point](../../../Murder/Core/Geometry/Point.html) \

#### SaveScreenShotArea(Rectangle)

```csharp
public void SaveScreenShotArea(Rectangle cameraRect)
```

Saves a screenshot of the specified camera area. Only records the request (`_takeScreenShot`); the actual capture happens inside `End()` via `TakeScreenshotIfNecessary`.

**Parameters** \
`cameraRect` [Rectangle](../../../Murder/Core/Geometry/Rectangle.html) \

#### SetupRenderTarget(RenderTarget2D, string, int, int, bool)

```csharp
protected RenderTarget2D SetupRenderTarget(RenderTarget2D existingTarget, string name, int width, int height, bool preserveContents)
```

Sets up a new RenderTarget2D, disposing of the existing one if necessary.

**Parameters** \
`existingTarget` [RenderTarget2D](https://docs.monogame.net/api/Microsoft.Xna.Framework.Graphics.RenderTarget2D.html) \
The existing RenderTarget2D to be disposed. \
`name` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
A debug name for the new RenderTarget2D. \
`width` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
Width of the new RenderTarget2D. \
`height` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
Height of the new RenderTarget2D. \
`preserveContents` [bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
Whether to preserve the contents in the new RenderTarget2D. \

**Returns** \
A new instance of RenderTarget2D. \
[RenderTarget2D](https://docs.monogame.net/api/Microsoft.Xna.Framework.Graphics.RenderTarget2D.html) \

#### TakeScreenshotIfNecessary(RenderTarget2D)

```csharp
protected void TakeScreenshotIfNecessary(RenderTarget2D target)
```

If a screenshot area was requested via `SaveScreenShotArea`, captures that camera-space area out of `target` into a temporary render target and saves it to disk via `SaveScreenshot`, then clears the pending request. No-op if no screenshot was requested. Called from `End()` right after the gameplay batch is drawn into `target`.

**Parameters** \
`target` [RenderTarget2D](https://docs.monogame.net/api/Microsoft.Xna.Framework.Graphics.RenderTarget2D.html) \

#### Unload()

```csharp
public void Unload()
```

Unload the render context.
Called when the render context is no longer being actively displayed. Disposes all resources, resets the `Camera`, calls the `UnloadImpl` extension point for derived classes, and clears the active render target on the `GraphicsDevice`.

#### UnloadImpl()

```csharp
protected virtual void UnloadImpl()
```

Override for custom unload implementations in derived classes.

#### UpdateViewport()

```csharp
protected virtual void UpdateViewport()
```

(Re)allocates all of this context's base render targets — `_uiTarget`, `_mainTarget`, `_tempTarget`, `_debugTarget`, and `_finalTarget` — sized to the current `Camera` dimensions (padded by `CAMERA_BLEED`) and `Viewport` output size, disposing any previous targets. Called from `Begin()` whenever the viewport is dirty (first frame, or after `OnViewportChanged`/a window resize). Override to also (re)allocate any additional targets a derived render context owns, calling `base.UpdateViewport()` first. Note this member is `protected`, not `public` — code outside a derived `RenderContext` should call `OnViewportChanged()` instead of invoking this directly.

⚡
