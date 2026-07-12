# Scene

**Namespace:** Murder.Core \
**Assembly:** Murder.dll

```csharp
public abstract class Scene : IDisposable
```

Abstract base class for all game scenes. Owns and drives an ECS `MonoWorld` and its `RenderContext` through the full lifecycle: initialize, load content, start, update/fixed-update, draw, suspend/resume, and unload.

**Intent:** `SceneLoader` owns the currently active `Scene` and calls into these lifecycle methods once per frame; `Scene` is the top-level container for a single game state (menu, level, cutscene).

**Use-case:** Most games only ever need `GameScene` (which loads its `World` from a `WorldAsset`); subclass `Scene` directly only for non-world screens such as a splash screen or a menu that doesn't need a full ECS world. Hand the instance to `SceneLoader` to drive the game loop for a given state.

**Implements:** _[IDisposable](https://learn.microsoft.com/en-us/dotnet/api/System.IDisposable?view=net-7.0)_

### ⭐ Constructors

```csharp
protected Scene()
```

### ⭐ Properties

#### \_calledStart

```csharp
protected bool _calledStart;
```

Tracks whether `Start` has already run for the current load, so `Update`/`FixedUpdate` know to call it lazily on first tick instead of requiring an explicit call.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### Loaded

```csharp
public bool Loaded { get; private set; }
```

Whether `LoadContent` has completed for this scene. Set to `false` for a freshly-constructed scene and back to `true` once content finishes loading.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### RenderContext

```csharp
public RenderContext? RenderContext { get; private set; }
```

Context renderer unique to this scene.

**Returns** \
[RenderContext](../../Murder/Core/Graphics/RenderContext.html) \

#### World

```csharp
public abstract MonoWorld? World { get; }
```

The ECS world driven by this scene, or `null` for scenes that don't need one (e.g. a plain menu screen). Implementors create and own this instance, typically inside `LoadContentImpl`.

**Returns** \
[MonoWorld](../../Murder/Core/MonoWorld.html) \

### ⭐ Methods

#### Dispose()

```csharp
public virtual void Dispose()
```

Disposes the scene, releasing the `RenderContext` and its underlying GPU resources.

#### DrawEnd()

```csharp
public void DrawEnd()
```

Ends the frame started by `DrawStart`, flushing the `RenderContext`'s render batches to the screen. Only call this after a `DrawStart` call that returned `true`.

#### DrawGui()

```csharp
public virtual void DrawGui()
```

Scenes that would like to implement a Gui should use this method.

#### DrawStart()

```csharp
public virtual bool DrawStart()
```

Begins rendering this scene's frame: calls `OnBeforeDraw`, opens the `RenderContext` render batches, and draws `World`'s render systems. Must be paired with a matching call to `DrawEnd`. Does nothing (and returns `false`) if `World` is `null` or `Start` hasn't run yet, so callers should check the return value before assuming a frame was actually drawn.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### FixedUpdate()

```csharp
public virtual void FixedUpdate()
```

Called at a fixed timestep (independent of frame rate) to tick `World`'s fixed-update systems — the right place for physics and other time-sensitive logic. Lazily calls `Start` first if it hasn't run yet for this load.

#### Initialize(GraphicsDevice, RenderContextFlags)

```csharp
public virtual void Initialize(GraphicsDevice graphics, RenderContextFlags flags)
```

Creates this scene's `RenderContext` for the given graphics device, sized to `Game.DefaultWidth`x`Game.DefaultHeight`. Called by `SceneLoader` right after a scene becomes active, before `LoadContent`.

**Parameters** \
`graphics` [GraphicsDevice](https://docs.monogame.net/api/Microsoft.Xna.Framework.Graphics.GraphicsDevice.html) \
`flags` [RenderContextFlags](../../Murder/Core/Graphics/RenderContextFlags.html) \

#### LoadContentImpl()

```csharp
public virtual void LoadContentImpl()
```

Override to load scene-specific content (textures, the ECS `World`, etc.) after `Initialize` has created the render context. This is where `GameScene` deserializes its `WorldAsset` and creates the runtime `MonoWorld`.

#### OnBeforeDraw()

```csharp
public virtual void OnBeforeDraw()
```

Called immediately before `DrawStart` actually begins rendering, giving the scene a chance to perform pre-draw preparation via `World`'s `PreDraw` systems. No-ops if `World` is `null` or `Start` hasn't run yet.

#### OnClientWindowChanged(Point)

```csharp
public virtual void OnClientWindowChanged(Point viewportSize)
```

Refresh the window size, updating the camera and render context. Shorthand for `OnClientWindowChanged(WindowChangeSettings)` using default settings for the new size.

**Parameters** \
`viewportSize` [Point](../../Murder/Core/Geometry/Point.html) \

#### OnClientWindowChanged(WindowChangeSettings)

```csharp
public virtual void OnClientWindowChanged(WindowChangeSettings settings)
```

Refresh the window/render context for the given `settings` (new viewport size and/or scaling), then notifies any listeners registered via `AddOnWindowRefresh`. Called whenever the game window is resized or the render scale changes.

**Parameters** \
`settings` [WindowChangeSettings](../../Murder/Core/Graphics/WindowChangeSettings.html) \

#### ReloadImpl()

```csharp
public virtual void ReloadImpl()
```

Override to handle hot-reload logic when source content changes during development, or to reset scene state on `Reload`.

#### ResumeImpl()

```csharp
public virtual void ResumeImpl()
```

Override to restore scene state when returning from a suspended state (e.g., re-entering from a pause menu).

#### Start()

```csharp
public virtual void Start()
```

Called once, the first time this scene is updated after content is loaded (or explicitly by a subclass). Runs all start systems in `World` and marks `_calledStart` so subsequent `Update`/`FixedUpdate` calls don't call it again.

#### SuspendImpl()

```csharp
public virtual void SuspendImpl()
```

Override to save or freeze scene state when the scene is temporarily suspended.

#### Update()

```csharp
public virtual void Update()
```

Called every frame to tick `World`'s update systems. Lazily calls `Start` first if it hasn't run yet for this load.

#### UnloadAsyncImpl()

```csharp
protected virtual Task UnloadAsyncImpl()
```

Override to perform asynchronous resource unloading when the scene exits. Invoked (but not awaited) by `Unload`.

**Returns** \
[Task](https://learn.microsoft.com/en-us/dotnet/api/System.Threading.Tasks.Task?view=net-7.0) \

#### AddOnWindowRefresh(Action)

```csharp
public void AddOnWindowRefresh(Action notification)
```

This will trigger UI refresh operations.

**Parameters** \
`notification` [Action](https://learn.microsoft.com/en-us/dotnet/api/System.Action?view=net-7.0) \

#### LoadContent()

```csharp
public void LoadContent()
```

Loads this scene's content by calling `LoadContentImpl`, logs the loaded world's name (if `World` resolves to a `WorldAsset`), resets the start flag, and marks `Loaded` as `true`. Called once by `SceneLoader.LoadContent` after `Initialize`.

#### Reload()

```csharp
public void Reload()
```

Reload the active scene.

#### ResetWindowRefreshEvents()

```csharp
public void ResetWindowRefreshEvents()
```

This will reset all watchers of trackers.

#### Resume()

```csharp
public void Resume()
```

Resumes the scene from a suspended state. Currently a no-op wrapper; override `ResumeImpl` to add behavior.

#### Suspend()

```csharp
public void Suspend()
```

Rests the current scene temporarily.

#### Unload()

```csharp
public void Unload()
```

Unloads this scene: releases the `RenderContext`'s GPU resources, clears window refresh listeners, and fires (without awaiting) `UnloadAsyncImpl` for any additional asynchronous cleanup. Called by `SceneLoader` right before switching to a different scene.

⚡
