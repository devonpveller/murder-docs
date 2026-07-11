# SceneLoader

**Namespace:** Murder.Core \
**Assembly:** Murder.dll

```csharp
public class SceneLoader
```

Orchestrates scene transitions and drives the active scene's lifecycle (initialize, load content, update, switch). Typically owned by the `Game` instance.

**Intent:** Central coordinator that manages which `Scene` is active and handles switching between scenes safely.

**Use-case:** Call `SwitchScene` to transition to a different level or menu, and `LoadContent`/`Initialize` during startup to bootstrap the initial scene.

### ⭐ Constructors
```csharp
public SceneLoader(GraphicsDeviceManager graphics, GameProfile settings, Scene scene, bool isDiagnosticEnabled)
```

Creates a new `SceneLoader` with the given graphics device, game profile, initial scene, and diagnostics flag.

**Parameters** \
`graphics` [GraphicsDeviceManager](https://docs.monogame.net/api/Microsoft.Xna.Framework.GraphicsDeviceManager.html) \
`settings` [GameProfile](../../Murder/Assets/GameProfile.html) \
`scene` [Scene](../../Murder/Core/Scene.html) \
`isDiagnosticEnabled` [bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

### ⭐ Properties
#### _graphics
```csharp
protected readonly GraphicsDeviceManager _graphics;
```

The MonoGame graphics device manager used to create and resize the render context.

**Returns** \
[GraphicsDeviceManager](https://docs.monogame.net/api/Microsoft.Xna.Framework.GraphicsDeviceManager.html) \
#### _settings
```csharp
protected readonly GameProfile _settings;
```

The game profile settings (resolution, target FPS, etc.) applied when initializing scenes.

**Returns** \
[GameProfile](../../Murder/Assets/GameProfile.html) \
#### ActiveScene
```csharp
public Scene ActiveScene { get; }
```

The scene currently being updated and rendered.

**Returns** \
[Scene](../../Murder/Core/Scene.html) \
#### IsDiagnosticEnabled
```csharp
protected readonly bool IsDiagnosticEnabled;
```

Whether it will load a scene and a load context that has advanced diagnostic
            features enabled (which also implies in more processing overhead).

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
### ⭐ Methods
#### ReplaceWorldOnCurrentScene(MonoWorld, bool)
```csharp
public bool ReplaceWorldOnCurrentScene(MonoWorld world, bool disposeWorld)
```

Replaces the world in the currently active scene with the given world.

**Parameters** \
`world` [MonoWorld](../../Murder/Core/MonoWorld.html) \
`disposeWorld` [bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### Initialize()
```csharp
public void Initialize()
```

Initialize current active scene.

#### LoadContent()
```csharp
public void LoadContent()
```

Load the content of the current active scene.

#### SwitchScene()
```csharp
public void SwitchScene()
```

Switch to a scene of type <typeparamref name="T" />.

#### SwitchScene(Scene)
```csharp
public void SwitchScene(Scene scene)
```

Switch to <paramref name="scene" />.

**Parameters** \
`scene` [Scene](../../Murder/Core/Scene.html) \

#### SwitchScene(Guid)
```csharp
public void SwitchScene(Guid worldGuid)
```

Switches to a `GameScene` backed by the `WorldAsset` identified by `worldGuid`.

**Parameters** \
`worldGuid` [Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \



⚡