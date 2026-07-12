# GameScene

**Namespace:** Murder.Core \
**Assembly:** Murder.dll

```csharp
public class GameScene : Scene, IDisposable
```

The standard `Scene` implementation used to play a level: it loads and hosts a `MonoWorld` built from a serialized `WorldAsset`, streams in the atlas textures the world references, drives the ECS simulation frame to frame, and unloads everything (including the world's atlases) when the scene is torn down.

**Intent:** The concrete scene type that wraps a serialized world asset for gameplay. Game code virtually never subclasses `GameScene`; it is instantiated directly with the GUID of the world to play.

**Use-case:** Instantiate with a `WorldAsset` GUID and pass to `SceneLoader.SwitchScene`/`SceneLoader.PushScene` (or however the game's scene stack is managed) to transition into a new game level.

**Implements:** _[Scene](../../Murder/Core/Scene.html), [IDisposable](https://learn.microsoft.com/en-us/dotnet/api/System.IDisposable?view=net-7.0)_

### ⭐ Constructors

```csharp
public GameScene(Guid guid)
```

Creates a scene that will load and play the `WorldAsset` identified by `guid`. The world itself is not built until `LoadContent` is called.

**Parameters** \
`guid` [Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \

### ⭐ Properties

#### \_calledStart

```csharp
protected bool _calledStart;
```

Inherited from `Scene`. Tracks whether `Start()` has already been called on this scene, so `Update`/`FixedUpdate` know to call it lazily on their first invocation instead of requiring an explicit separate start step.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### Loaded

```csharp
public bool Loaded { get; }
```

Inherited from `Scene`. Whether this scene's content has been fully loaded (i.e. `LoadContent` has run) and is ready to update and render.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### RenderContext

```csharp
public RenderContext? RenderContext { get; }
```

Inherited from `Scene`. The rendering context associated with this scene (created by `Initialize`), used to draw batches to the screen. `null` until `Initialize` has run.

**Returns** \
[RenderContext](../../Murder/Core/Graphics/RenderContext.html) \

#### World

```csharp
public override MonoWorld? World { get; }
```

The active ECS world for this scene, or `null` before `LoadContent` has run or after the scene has been unloaded/reloaded. Overrides the abstract `World` property from `Scene`, backing it with the world built by `LoadContentImpl`.

**Returns** \
[MonoWorld](../../Murder/Core/MonoWorld.html) \

#### WorldGuid

```csharp
public Guid WorldGuid { get; }
```

The GUID of the `WorldAsset` this scene was created from. Used to look the asset back up (e.g. to resolve its referenced atlases) and to re-create the world on reload.

**Returns** \
[Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \

### ⭐ Methods

#### UnloadAsyncImpl()

```csharp
protected override async Task UnloadAsyncImpl()
```

Disposes of atlases loaded exclusively for this world (skipping any flagged with `ReferencedAtlas.UnloadOnExit == false`), waits for any pending save (`Game.Data.PendingSave`) to finish, and then disposes the previous `MonoWorld`. The world reference is nulled out immediately so nothing can observe or mutate a world that is mid-teardown. Called by the inherited `Unload()`.

**Returns** \
[Task](https://learn.microsoft.com/en-us/dotnet/api/System.Threading.Tasks.Task?view=net-7.0) \

#### AddOnWindowRefresh(Action)

```csharp
public void AddOnWindowRefresh(Action notification)
```

Inherited from `Scene`. Registers a callback that fires whenever the window/UI refreshes (`OnClientWindowChanged`). Do not perform operations that rely on the main thread from the callback.

**Parameters** \
`notification` [Action](https://learn.microsoft.com/en-us/dotnet/api/System.Action?view=net-7.0) \

#### Dispose()

```csharp
public virtual void Dispose()
```

Inherited from `Scene`. Disposes the scene's `RenderContext`.

#### DrawEnd()

```csharp
public void DrawEnd()
```

Inherited from `Scene`. Ends the batches opened by `DrawStart()`, flushing them to the screen. Must be paired with a preceding `DrawStart()` call.

#### DrawGui()

```csharp
public virtual void DrawGui()
```

Inherited from `Scene`. Runs the world's GUI render systems (`MonoWorld.DrawGui`) if the scene has already started. Intended for scenes/systems that draw UI on top of the world.

#### DrawStart()

```csharp
public virtual bool DrawStart()
```

Inherited from `Scene`. Calls `OnBeforeDraw()`, begins the `RenderContext`, and runs the world's render systems (`MonoWorld.Draw`). Returns `false` (without drawing) if the world is `null` or `Start()` has not run yet.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### FixedUpdate()

```csharp
public virtual void FixedUpdate()
```

Inherited from `Scene`. Calls `Start()` on first invocation if it hasn't run yet, then runs the world's fixed-update systems (`MonoWorld.FixedUpdate`).

#### Initialize(GraphicsDevice, RenderContextFlags)

```csharp
public virtual void Initialize(GraphicsDevice graphics, RenderContextFlags flags)
```

Inherited from `Scene`. Creates the scene's `RenderContext` via `Game.Instance.CreateRenderContext`, sized to `Game.DefaultWidth`/`Game.DefaultHeight`. Called once by the engine before the scene's content is loaded.

**Parameters** \
`graphics` [GraphicsDevice](https://docs.monogame.net/api/Microsoft.Xna.Framework.Graphics.GraphicsDevice.html) \
`flags` [RenderContextFlags](../../Murder/Core/Graphics/RenderContextFlags.html) \

#### LoadContent()

```csharp
public void LoadContent()
```

Inherited from `Scene`. Calls `LoadContentImpl()`, logs the loaded world's name if one was created, and marks the scene as `Loaded`. This is the entry point the engine calls when transitioning into the scene.

#### LoadContentImpl()

```csharp
public override void LoadContentImpl()
```

Builds the `MonoWorld` from the referenced `WorldAsset` (via `Game.Data.CreateWorldInstanceFromSave`) and eagerly loads the textures for every atlas the world references, so the first frame does not stall on texture I/O. Forces a generation-0 GC afterwards to reclaim the garbage produced while instantiating entities/components.

#### OnBeforeDraw()

```csharp
public virtual void OnBeforeDraw()
```

Inherited from `Scene`. Runs the world's pre-render systems (`MonoWorld.PreDraw`) if the world exists and the scene has started. Called automatically by `DrawStart()`.

#### OnClientWindowChanged(Point)

```csharp
public virtual void OnClientWindowChanged(Point viewportSize)
```

Inherited from `Scene`. Convenience overload that wraps `viewportSize` into a `WindowChangeSettings` and forwards to `OnClientWindowChanged(WindowChangeSettings)`.

**Parameters** \
`viewportSize` [Point](../../Murder/Core/Geometry/Point.html) \

#### OnClientWindowChanged(WindowChangeSettings)

```csharp
public virtual void OnClientWindowChanged(WindowChangeSettings settings)
```

Inherited from `Scene`. Notifies the `RenderContext` of the window size/settings change and invokes any callbacks registered via `AddOnWindowRefresh`. Call this (or the `Point` overload) whenever the game window is resized or display settings change.

**Parameters** \
`settings` [WindowChangeSettings](../../Murder/Core/Graphics/WindowChangeSettings.html) \

#### Reload()

```csharp
public void Reload()
```

Inherited from `Scene`. Resets `_calledStart` and calls `ReloadImpl()`. Use this to force a scene to rebuild its world from scratch (e.g. after a hot-reload or when restarting a level).

#### ReloadImpl()

```csharp
public override void ReloadImpl()
```

Discards the current world reference so the next `Reload()` cycle rebuilds it from scratch via `LoadContentImpl()`.

#### ReplaceWorld(MonoWorld, bool)

```csharp
public bool ReplaceWorld(MonoWorld world, bool disposeWorld)
```

Swaps in a new `MonoWorld` for this scene, optionally disposing the previous one. Used by tooling/hot-reload flows that need to hand the scene an already-constructed world instead of going through `LoadContentImpl`.

**Parameters** \
`world` [MonoWorld](../../Murder/Core/MonoWorld.html) \
`disposeWorld` [bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### ResetWindowRefreshEvents()

```csharp
public void ResetWindowRefreshEvents()
```

Inherited from `Scene`. Clears all window-refresh watchers previously registered via `AddOnWindowRefresh`. Called as part of `Unload()`.

#### Resume()

```csharp
public void Resume()
```

Inherited from `Scene`. Public entry point for resuming the scene; calls `ResumeImpl()`.

#### ResumeImpl()

```csharp
public override void ResumeImpl()
```

Re-activates every system in the world that was deactivated by `SuspendImpl` (`MonoWorld.ActivateAllSystems`), resuming simulation when the scene becomes the active one again (e.g. returning from a paused sub-scene).

#### Start()

```csharp
public virtual void Start()
```

Inherited from `Scene`. Calls `World.Start()` (running every `IStartupSystem`) and marks `_calledStart` as `true`. Invoked lazily by `Update`/`FixedUpdate`/`DrawStart` on their first call after load.

#### Suspend()

```csharp
public void Suspend()
```

Inherited from `Scene`. Public entry point for suspending the scene; calls `SuspendImpl()`.

#### SuspendImpl()

```csharp
public override void SuspendImpl()
```

Deactivates every system in the world (`MonoWorld.DeactivateAllSystems`), effectively freezing simulation while this scene is not the one being actively played (e.g. while another scene is on top of it).

#### Unload()

```csharp
public void Unload()
```

Inherited from `Scene`. Unloads the `RenderContext`, resets window-refresh watchers, and kicks off `UnloadAsyncImpl()`.

#### Update()

```csharp
public virtual void Update()
```

Inherited from `Scene`. Calls `Start()` on first invocation if it hasn't run yet, then runs the world's update systems (`MonoWorld.Update`).

⚡
