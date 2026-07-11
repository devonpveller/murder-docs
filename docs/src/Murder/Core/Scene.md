# Scene

**Namespace:** Murder.Core \
**Assembly:** Murder.dll

```csharp
public abstract class Scene : IDisposable
```

Abstract base class for all game scenes. Manages the lifecycle of a `MonoWorld` including initialization, content loading, updating, drawing, suspension, and unloading.

**Intent:** The top-level container for a single game state (menu, level, cutscene) that drives the ECS world through its lifetime.

**Use-case:** Subclass `Scene` (or use `GameScene` directly) and hand the instance to `SceneLoader` to drive the game loop for a given state.

**Implements:** _[IDisposable](https://learn.microsoft.com/en-us/dotnet/api/System.IDisposable?view=net-7.0)_

### ⭐ Constructors
```csharp
protected Scene()
```

### ⭐ Properties
#### _calledStart
```csharp
protected bool _calledStart;
```

Tracks whether `Start()` has been called, preventing double-initialization if the scene is resumed after suspension.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
#### Loaded
```csharp
public bool Loaded { get; private set; }
```

Whether this scene's content has been fully loaded and is ready to update and render.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
#### RenderContext
```csharp
public RenderContext RenderContext { get; private set; }
```

Context renderer unique to this scene.

**Returns** \
[RenderContext](../../Murder/Core/Graphics/RenderContext.html) \
#### World
```csharp
public abstract virtual MonoWorld World { get; }
```

The active ECS world for this scene. Implementors create and own this instance.

**Returns** \
[MonoWorld](../../Murder/Core/MonoWorld.html) \
### ⭐ Methods
#### UnloadAsyncImpl()
```csharp
public virtual Task UnloadAsyncImpl()
```

Override to perform asynchronous resource unloading when the scene exits.

**Returns** \
[Task](https://learn.microsoft.com/en-us/dotnet/api/System.Threading.Tasks.Task?view=net-7.0) \

#### Dispose()
```csharp
public virtual void Dispose()
```

Disposes the scene and releases all held resources.

#### Draw()
```csharp
public virtual void Draw()
```

Called each frame to render the world via the render systems.

#### DrawGui()
```csharp
public virtual void DrawGui()
```

Scenes that would like to implement a Gui should use this method.

#### FixedUpdate()
```csharp
public virtual void FixedUpdate()
```

Called at a fixed timestep for physics and other time-sensitive logic.

#### Initialize(GraphicsDevice, GameProfile, RenderContextFlags)
```csharp
public virtual void Initialize(GraphicsDevice graphics, GameProfile settings, RenderContextFlags flags)
```

Initializes the scene's `RenderContext` with the given graphics device and profile settings.

**Parameters** \
`graphics` [GraphicsDevice](https://docs.monogame.net/api/Microsoft.Xna.Framework.Graphics.GraphicsDevice.html) \
`settings` [GameProfile](../../Murder/Assets/GameProfile.html) \
`flags` [RenderContextFlags](../../Murder/Core/Graphics/RenderContextFlags.html) \

#### LoadContentImpl()
```csharp
public virtual void LoadContentImpl()
```

Override to load scene-specific content (textures, worlds, etc.) after initialization.

#### OnBeforeDraw()
```csharp
public virtual void OnBeforeDraw()
```

Called immediately before `Draw`, giving the scene a chance to perform pre-draw preparation.

#### RefreshWindow(Point, GraphicsDevice, GameProfile)
```csharp
public virtual void RefreshWindow(Point viewportSize, GraphicsDevice graphics, GameProfile settings)
```

Refresh the window size, updating the camera and render context.

**Parameters** \
`viewportSize` [Point](../../Murder/Core/Geometry/Point.html) \
\
`graphics` [GraphicsDevice](https://docs.monogame.net/api/Microsoft.Xna.Framework.Graphics.GraphicsDevice.html) \
\
`settings` [GameProfile](../../Murder/Assets/GameProfile.html) \
\

#### ReloadImpl()
```csharp
public virtual void ReloadImpl()
```

Override to handle hot-reload logic when source content changes during development.

#### ResumeImpl()
```csharp
public virtual void ResumeImpl()
```

Override to restore scene state when returning from a suspended state (e.g., re-entering from a pause menu).

#### Start()
```csharp
public virtual void Start()
```

Called once after content is loaded; runs all start systems in the world.

#### SuspendImpl()
```csharp
public virtual void SuspendImpl()
```

Override to save or freeze scene state when the scene is temporarily suspended.

#### Update()
```csharp
public virtual void Update()
```

Called every frame to tick the world's update systems.

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

Loads the scene's content and marks it as `Loaded = true`.

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

Resumes the scene from a suspended state.

#### Suspend()
```csharp
public void Suspend()
```

Rests the current scene temporarily.

#### Unload()
```csharp
public void Unload()
```

Asynchronously unloads the scene content and disposes the world.



⚡