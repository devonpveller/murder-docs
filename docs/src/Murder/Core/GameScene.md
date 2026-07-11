# GameScene

**Namespace:** Murder.Core \
**Assembly:** Murder.dll

```csharp
public class GameScene : Scene, IDisposable
```

A concrete `Scene` implementation that loads and hosts a `MonoWorld` identified by a `WorldAsset` GUID. It handles loading the atlas textures referenced by the world, running the ECS simulation, and unloading resources on exit.

**Intent:** The standard scene type that wraps a serialized world asset for gameplay.

**Use-case:** Instantiate with a world asset GUID and pass to the `SceneLoader` to transition into a new game level.

**Implements:** _[Scene](../../Murder/Core/Scene.html), [IDisposable](https://learn.microsoft.com/en-us/dotnet/api/System.IDisposable?view=net-7.0)_

### ⭐ Constructors
```csharp
public GameScene(Guid guid)
```

**Parameters** \
`guid` [Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \

### ⭐ Properties
#### _calledStart
```csharp
protected bool _calledStart;
```

Tracks whether `Start()` has already been called on this scene to prevent double-initialization.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
#### Loaded
```csharp
public bool Loaded { get; }
```

Whether this scene's content has been fully loaded and is ready to update and render.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
#### RenderContext
```csharp
public RenderContext RenderContext { get; }
```

The rendering context associated with this scene, used to draw batches to the screen.

**Returns** \
[RenderContext](../../Murder/Core/Graphics/RenderContext.html) \
#### World
```csharp
public virtual MonoWorld World { get; }
```

The active ECS world for this scene. May be `null` before content is loaded or after the scene is unloaded.

**Returns** \
[MonoWorld](../../Murder/Core/MonoWorld.html) \
#### WorldGuid
```csharp
public Guid WorldGuid { get; }
```

The GUID of the `WorldAsset` this scene was created from.

**Returns** \
[Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \
### ⭐ Methods
#### ReplaceWorld(MonoWorld, bool)
```csharp
public bool ReplaceWorld(MonoWorld world, bool disposeWorld)
```

Replace world and return the previous one, which should be disposed.

**Parameters** \
`world` [MonoWorld](../../Murder/Core/MonoWorld.html) \
`disposeWorld` [bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### UnloadAsyncImpl()
```csharp
public virtual Task UnloadAsyncImpl()
```

Asynchronously disposes the current world and unloads atlas textures that were loaded for this scene.

**Returns** \
[Task](https://learn.microsoft.com/en-us/dotnet/api/System.Threading.Tasks.Task?view=net-7.0) \

#### Dispose()
```csharp
public virtual void Dispose()
```

#### Draw()
```csharp
public virtual void Draw()
```

#### DrawGui()
```csharp
public virtual void DrawGui()
```

#### FixedUpdate()
```csharp
public virtual void FixedUpdate()
```

#### Initialize(GraphicsDevice, GameProfile, RenderContextFlags)
```csharp
public virtual void Initialize(GraphicsDevice graphics, GameProfile settings, RenderContextFlags flags)
```

**Parameters** \
`graphics` [GraphicsDevice](https://docs.monogame.net/api/Microsoft.Xna.Framework.Graphics.GraphicsDevice.html) \
`settings` [GameProfile](../../Murder/Assets/GameProfile.html) \
`flags` [RenderContextFlags](../../Murder/Core/Graphics/RenderContextFlags.html) \

#### LoadContentImpl()
```csharp
public virtual void LoadContentImpl()
```

#### OnBeforeDraw()
```csharp
public virtual void OnBeforeDraw()
```

#### RefreshWindow(Point, GraphicsDevice, GameProfile)
```csharp
public virtual void RefreshWindow(Point viewportSize, GraphicsDevice graphics, GameProfile settings)
```

**Parameters** \
`viewportSize` [Point](../../Murder/Core/Geometry/Point.html) \
`graphics` [GraphicsDevice](https://docs.monogame.net/api/Microsoft.Xna.Framework.Graphics.GraphicsDevice.html) \
`settings` [GameProfile](../../Murder/Assets/GameProfile.html) \

#### ReloadImpl()
```csharp
public virtual void ReloadImpl()
```

#### ResumeImpl()
```csharp
public virtual void ResumeImpl()
```

#### Start()
```csharp
public virtual void Start()
```

#### SuspendImpl()
```csharp
public virtual void SuspendImpl()
```

#### Update()
```csharp
public virtual void Update()
```

#### AddOnWindowRefresh(Action)
```csharp
public void AddOnWindowRefresh(Action notification)
```

**Parameters** \
`notification` [Action](https://learn.microsoft.com/en-us/dotnet/api/System.Action?view=net-7.0) \

#### LoadContent()
```csharp
public void LoadContent()
```

#### Reload()
```csharp
public void Reload()
```

#### ResetWindowRefreshEvents()
```csharp
public void ResetWindowRefreshEvents()
```

#### Resume()
```csharp
public void Resume()
```

#### Suspend()
```csharp
public void Suspend()
```

#### Unload()
```csharp
public void Unload()
```



⚡