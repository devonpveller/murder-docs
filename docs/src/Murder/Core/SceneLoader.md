# SceneLoader

**Namespace:** Murder.Core \
**Assembly:** Murder.dll

```csharp
public class SceneLoader
```

Orchestrates scene transitions and drives the currently active `Scene`'s lifecycle (initialize, load content, switch). Typically owned by the `Game` instance, which forwards its own `Update`/`Draw` calls into `ActiveScene`.

**Intent:** Central coordinator that manages which `Scene` is active and handles switching between scenes safely. Also caches every `GameScene` (keyed by world GUID) and generic `Scene` subtype it has ever switched to, so switching back to a previously-visited scene reuses the existing instance (calling `Reload` on it) instead of recreating it from scratch.

**Use-case:** Call `SwitchScene(Guid)` to transition to a level backed by a `WorldAsset`, or `SwitchScene<T>()` to transition to a non-world scene such as a menu or splash screen. Call `LoadContent`/`Initialize` during startup to bootstrap the initial scene.

### ⭐ Constructors

```csharp
public SceneLoader(GraphicsDeviceManager graphics, GameProfile settings, Scene scene, bool isDiagnosticEnabled)
```

Creates a scene loader and immediately activates `scene` (unloading any previous active scene and calling `Initialize` on the new one).

**Parameters** \
`graphics` [GraphicsDeviceManager](https://docs.monogame.net/api/Microsoft.Xna.Framework.GraphicsDeviceManager.html) \
`settings` [GameProfile](../../Murder/Assets/GameProfile.html) \
`scene` [Scene](../../Murder/Core/Scene.html) \
`isDiagnosticEnabled` [bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

### ⭐ Properties

#### \_graphics

```csharp
protected readonly GraphicsDeviceManager _graphics;
```

The MonoGame graphics device manager used to create and resize the render context.

**Returns** \
[GraphicsDeviceManager](https://docs.monogame.net/api/Microsoft.Xna.Framework.GraphicsDeviceManager.html) \

#### \_settings

```csharp
protected readonly GameProfile _settings;
```

The game profile settings (resolution, target FPS, etc.) captured at construction time.

**Returns** \
[GameProfile](../../Murder/Assets/GameProfile.html) \

#### ActiveScene

```csharp
public Scene ActiveScene { get; }
```

The scene currently being updated and rendered. Set via the constructor or one of the `SwitchScene` overloads.

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

Swaps the ECS world of the currently active scene for `world`, without going through the normal asset-loading path. Only works when the active scene is a `GameScene`; used by tools/hot-reload flows that need to hand the loader an already-constructed world (e.g. the editor swapping in a modified world while play-testing).

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

#### SwitchScene\<T\>()

```csharp
public void SwitchScene<T>()
```

Switch to a scene of type `T`, for non-world scenes such as a menu or splash screen. If a scene of this type was switched to before, reuses and reloads the cached instance instead of constructing a new one via `T`'s parameterless constructor.

#### SwitchScene(Scene)

```csharp
public void SwitchScene(Scene scene)
```

Switch to `scene`.

**Parameters** \
`scene` [Scene](../../Murder/Core/Scene.html) \

#### SwitchScene(Guid)

```csharp
public void SwitchScene(Guid worldGuid)
```

Switches to a `GameScene` backed by the `WorldAsset` identified by `worldGuid`. If that world was already loaded before, reuses and reloads the cached `GameScene` instance instead of constructing a new one.

**Parameters** \
`worldGuid` [Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \

⚡
