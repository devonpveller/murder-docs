# Game

**Namespace:** Murder \
**Assembly:** Murder.dll

```csharp
public class Game : Game, IDisposable
```

**Implements:** _[Game](https://docs.monogame.net/api/Microsoft.Xna.Framework.Game.html), [IDisposable](https://learn.microsoft.com/en-us/dotnet/api/System.IDisposable?view=net-7.0)_

**Intent:** `Game` is the singleton root of the Murder engine. It owns the MonoGame game loop, the active scene/world, all timing state, and top-level subsystem references (input, sound, data, graphics). Every game built on Murder instantiates exactly one `Game` (or a derived editor `Architect` subclass).

**Use-case:** Instantiate `Game` with your `IMurderGame` implementation and call `Run()`. Access global state via static helpers such as `Game.Data`, `Game.Input`, `Game.Sound`, `Game.Now`, and `Game.Profile`. To switch levels call `QueueWorldTransition(Guid)`. Pause/resume timing with `Pause()` / `Resume()`. Use `FreezeFrames(n)` for screen-shake or hit-stop effects.

### ⭐ Constructors
```csharp
public Game(IMurderGame game, GameDataManager dataManager)
```

Creates a new game, there should only be one game instance ever.
            If <paramref name="dataManager" /> is not initialized, it will create the starting scene from [GameProfile](../Murder/Assets/GameProfile.html).

**Parameters** \
`game` [IMurderGame](../Murder/IMurderGame.html) \
`dataManager` [GameDataManager](../Murder/Data/GameDataManager.html) \

```csharp
public Game(IMurderGame game)
```

**Parameters** \
`game` [IMurderGame](../Murder/IMurderGame.html) \

### ⭐ Properties
#### _disposePendingWorld
```csharp
protected bool _disposePendingWorld;
```

When `true`, the world stored in `_pendingWorld` will be disposed (rather than recycled) once it is replaced by the next pending world. Set automatically during world transitions.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
#### _gameData
```csharp
protected readonly GameDataManager _gameData;
```

The central asset and save-data manager for this game instance. Accessible publicly via the static `Game.Data` shortcut.

**Returns** \
[GameDataManager](../Murder/Data/GameDataManager.html) \
#### _graphics
```csharp
protected readonly GraphicsDeviceManager _graphics;
```

MonoGame's `GraphicsDeviceManager` used to configure resolution, fullscreen mode, and V-sync. Exposed publicly via the `GraphicsDeviceManager` property and statically via `Game.GraphicsDevice`.

**Returns** \
[GraphicsDeviceManager](https://docs.monogame.net/api/Microsoft.Xna.Framework.GraphicsDeviceManager.html) \
#### _logger
```csharp
protected GameLogger _logger;
```

Single logger of the game.

**Returns** \
[GameLogger](../Murder/Diagnostics/GameLogger.html) \
#### _pendingExit
```csharp
protected bool _pendingExit;
```

Set to `true` by `QueueExitGame()`. The game loop checks this flag at the end of each update and calls `ExitGame()` safely, avoiding disposal of a world that is mid-update.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
#### _pendingWorld
```csharp
protected MonoWorld _pendingWorld;
```

A fully-initialized `MonoWorld` that is waiting to replace the current active world at the start of the next frame. Populated by `QueueReplaceWorldOnCurrentScene`.

**Returns** \
[MonoWorld](../Murder/Core/MonoWorld.html) \
#### _pendingWorldTransition
```csharp
protected T? _pendingWorldTransition;
```

**Returns** \
[T?](https://learn.microsoft.com/en-us/dotnet/api/System.Nullable-1?view=net-7.0) \
#### _playerInput
```csharp
protected readonly PlayerInput _playerInput;
```

The engine-wide input manager that tracks keyboard, mouse, and gamepad state. Accessible via the static `Game.Input` shortcut.

**Returns** \
[PlayerInput](../Murder/Core/Input/PlayerInput.html) \
#### _sceneLoader
```csharp
protected SceneLoader _sceneLoader;
```

Initialized in [Game.LoadContent](../Murder/Game.html#loadcontent).

**Returns** \
[SceneLoader](../Murder/Core/SceneLoader.html) \
#### ActiveScene
```csharp
public Scene ActiveScene { get; }
```

**Returns** \
[Scene](../Murder/Core/Scene.html) \
#### AlwaysUpdateBeforeFixed
```csharp
protected virtual bool AlwaysUpdateBeforeFixed { get; }
```

Always run update before fixed update. Override this for a different behavior.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
#### Components
```csharp
public GameComponentCollection Components { get; }
```

MonoGame's collection of `IGameComponent` objects that receive automatic `Initialize`, `Update`, and `Draw` calls. Rarely used directly in Murder; prefer ECS systems instead.

**Returns** \
[GameComponentCollection](https://docs.monogame.net/api/Microsoft.Xna.Framework.GameComponentCollection.html) \
#### Content
```csharp
public ContentManager Content { get; public set; }
```

MonoGame's `ContentManager` for loading XNB-compiled assets. Murder uses its own `GameDataManager` for most asset loading; this property is inherited from `Microsoft.Xna.Framework.Game`.

**Returns** \
[ContentManager](https://docs.monogame.net/api/Microsoft.Xna.Framework.Content.ContentManager.html) \
#### Data
```csharp
public static GameDataManager Data { get; }
```

Gets the GameDataManager instance.

**Returns** \
[GameDataManager](../Murder/Data/GameDataManager.html) \
#### DeltaTime
```csharp
public static float DeltaTime { get; }
```

De time difference between current and last update, scaled by pause and other time scaling. Value is reliable only during the Update().

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
#### DIAGNOSTICS_MODE
```csharp
public static bool DIAGNOSTICS_MODE;
```

Use this to set whether diagnostics should be pulled.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
#### Downsample
```csharp
public float Downsample;
```

Render-resolution scaling factor. A value of `1` renders at full resolution; values below `1` render to a smaller target and upscale, improving performance at the cost of quality. Modify before the scene loads to apply at startup.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
#### FixedDeltaTime
```csharp
public static float FixedDeltaTime { get; }
```

Gets the fixed delta time in seconds.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
#### Fullscreen
```csharp
public bool Fullscreen { get; public set; }
```

Gets or sets the fullscreen mode of the game.
            When set, it updates the game's window to reflect the new mode.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
#### GameScale
```csharp
public Vector2 GameScale { get; }
```

Gets the scale of the game relative to the window size and game profile scale.
            Returns Vector2.One if the window has invalid dimensions.

**Returns** \
[Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
#### GraphicsDevice
```csharp
public GraphicsDevice GraphicsDevice { get; }
```

Gets the current instance of the GraphicsDevice.

**Returns** \
[GraphicsDevice](https://docs.monogame.net/api/Microsoft.Xna.Framework.Graphics.GraphicsDevice.html) \
#### GraphicsDeviceManager
```csharp
public GraphicsDeviceManager GraphicsDeviceManager { get; }
```

Public accessor for the `_graphics` field. Use this to query or change graphics settings such as preferred back-buffer dimensions or fullscreen state.

**Returns** \
[GraphicsDeviceManager](https://docs.monogame.net/api/Microsoft.Xna.Framework.GraphicsDeviceManager.html) \
#### GraphLogger
```csharp
public virtual GraphLogger GraphLogger { get; }
```

Gets the current graph logger debugger.

**Returns** \
[GraphLogger](../Murder/Diagnostics/GraphLogger.html) \
#### Grid
```csharp
public static GridConfiguration Grid { get; }
```

Beautiful hardcoded grid so it's very easy to access in game!

**Returns** \
[GridConfiguration](../Murder/Core/GridConfiguration.html) \
#### HasCursor
```csharp
protected virtual bool HasCursor { get; }
```

Whether this game renders a visible cursor. Defaults to `false` in the base `Game`; the `IMurderGame` implementation controls this and the base class reads it to set `IsMouseVisible`. Override in a subclass if cursor visibility depends on runtime state.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
#### Height
```csharp
public static int Height { get; }
```

Gets the game height from the GameProfile. This is the intended size, not the actual size. For the current window size use [RenderContext.Camera](../Murder/Core/Graphics/RenderContext.html#camera).

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
#### InactiveSleepTime
```csharp
public TimeSpan InactiveSleepTime { get; public set; }
```

The duration the game sleeps per frame when the window is not the foreground application. Inherited from `Microsoft.Xna.Framework.Game`; increase to reduce CPU usage when the game is in the background.

**Returns** \
[TimeSpan](https://learn.microsoft.com/en-us/dotnet/api/System.TimeSpan?view=net-7.0) \
#### InitialScene
```csharp
protected virtual Scene InitialScene { get; }
```

The first `Scene` the engine creates when the game starts. Defaults to a `GameScene` loaded from `GameProfile.StartingScene`. Override in a subclass to launch with a different or custom scene.

**Returns** \
[Scene](../Murder/Core/Scene.html) \
#### Input
```csharp
public static PlayerInput Input { get; }
```

Gets the PlayerInput instance.

**Returns** \
[PlayerInput](../Murder/Core/Input/PlayerInput.html) \
#### Instance
```csharp
public static Game Instance { get; private set; }
```

Singleton instance of the game. wBe cautious when referencing this...

**Returns** \
[Game](../Murder/Game.html) \
#### IsActive
```csharp
public bool IsActive { get; internal set; }
```

`true` while the game window has OS focus. When `false` the game may sleep for `InactiveSleepTime` per frame. Fires `Activated` / `Deactivated` events on change.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
#### IsDiagnosticEnabled
```csharp
protected virtual bool IsDiagnosticEnabled { get; }
```

Whether the in-game diagnostic overlay is active. When `true`, per-system timing data is collected and displayed. The editor (`Architect`) overrides this to `true`.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
#### IsFixedTimeStep
```csharp
public bool IsFixedTimeStep { get; public set; }
```

When `true`, MonoGame attempts to call `Update` at exactly `TargetElapsedTime` intervals. Murder overrides timing internally, so this is typically left at its default. Inherited from `Microsoft.Xna.Framework.Game`.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
#### IsMouseVisible
```csharp
public bool IsMouseVisible { get; public set; }
```

Controls OS-level mouse cursor visibility. Murder sets this automatically from `HasCursor` during initialization. Inherited from `Microsoft.Xna.Framework.Game`.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
#### IsPaused
```csharp
public bool IsPaused { get; private set; }
```

`true` when the game has been paused via `Pause()`. While paused, `DeltaTime` is effectively zero and time does not advance. Resume normal play with `Resume()`.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
#### IsSkippingDeltaTimeOnUpdate
```csharp
public bool IsSkippingDeltaTimeOnUpdate { get; }
```

Whether the player is currently skipping frames (due to cutscene) and ignore
            the time while calling update methods.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
#### LaunchParameters
```csharp
public LaunchParameters LaunchParameters { get; }
```

Command-line arguments parsed by MonoGame at startup. Use to implement launch flags such as `-fullscreen` or `-nosound`. Inherited from `Microsoft.Xna.Framework.Game`.

**Returns** \
[LaunchParameters](https://docs.monogame.net/api/Microsoft.Xna.Framework.LaunchParameters.html) \
#### LONGEST_TIME_RESET
```csharp
public static const float LONGEST_TIME_RESET;
```

The number of seconds after which `LongestUpdateTime` and `LongestRenderTime` are automatically reset. Prevents stale spikes from dominating the diagnostic display indefinitely.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
#### LongestRenderTime
```csharp
public float LongestRenderTime { get; private set; }
```

Gets the longest render time ever recorded.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
#### LongestUpdateTime
```csharp
public float LongestUpdateTime { get; private set; }
```

The largest `UpdateTime` value ever recorded since the last `LONGEST_TIME_RESET` interval. Useful for identifying frame spikes in diagnostics.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
#### Now
```csharp
public static float Now { get; }
```

Gets the current scaled elapsed time.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
#### NowAbsolute
```csharp
public static float NowAbsolute { get; }
```

Gets the absolute time since the game started. This is not affected by pause, freeze frames or time scaling.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
#### NowUnscaled
```csharp
public static float NowUnscaled { get; }
```

Gets the current unscaled elapsed time.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
#### Preferences
```csharp
public static GamePreferences Preferences { get; }
```

Gets the GamePreferences asset instance.

**Returns** \
[GamePreferences](../Murder/Save/GamePreferences.html) \
#### PreviousElapsedTime
```csharp
public float PreviousElapsedTime { get; }
```

Elapsed time in seconds from the previous update frame since the game started

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
#### PreviousNow
```csharp
public static float PreviousNow { get; }
```

Gets the scaled elapsed time from the previous fixed update.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
#### PreviousNowUnscaled
```csharp
public static float PreviousNowUnscaled { get; }
```

Time from previous fixed update.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
#### Profile
```csharp
public static GameProfile Profile { get; }
```

Gets the GameProfile asset instance.

**Returns** \
[GameProfile](../Murder/Assets/GameProfile.html) \
#### Random
```csharp
public static Random Random;
```

Provides a static Random instance.

**Returns** \
[Random](https://learn.microsoft.com/en-us/dotnet/api/System.Random?view=net-7.0) \
#### RenderTime
```csharp
public float RenderTime { get; private set; }
```

Time in seconds that the Draw() method took to finish

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
#### Save
```csharp
public static SaveData Save { get; }
```

Gets the active SaveData asset instance.

**Returns** \
[SaveData](../Murder/Assets/SaveData.html) \
#### Services
```csharp
public GameServiceContainer Services { get; }
```

MonoGame's service-locator container for sharing objects between game components. Murder uses its own dependency-injection patterns (static accessors, `Game.Data`, etc.); this is primarily an inherited MonoGame surface.

**Returns** \
[GameServiceContainer](https://docs.monogame.net/api/Microsoft.Xna.Framework.GameServiceContainer.html) \
#### Sound
```csharp
public static ISoundPlayer Sound { get; }
```

Gets the ISoundPlayer instance.

**Returns** \
[ISoundPlayer](../Murder/Core/Sounds/ISoundPlayer.html) \
#### SoundPlayer
```csharp
public readonly ISoundPlayer SoundPlayer;
```

The concrete sound subsystem instance for this game. Created during `LoadContent` via `IMurderGame.CreateSoundPlayer()`. Access it globally via the `Game.Sound` static shortcut.

**Returns** \
[ISoundPlayer](../Murder/Core/Sounds/ISoundPlayer.html) \
#### StartedSkippingCutscene
```csharp
public bool StartedSkippingCutscene;
```

Whether the player started skipping.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
#### TargetElapsedTime
```csharp
public TimeSpan TargetElapsedTime { get; public set; }
```

Desired duration between frames when `IsFixedTimeStep` is `true`. Inherited from MonoGame. Murder uses its own delta-time accumulation independently of this.

**Returns** \
[TimeSpan](https://learn.microsoft.com/en-us/dotnet/api/System.TimeSpan?view=net-7.0) \
#### TimeScale
```csharp
public float TimeScale;
```

Multiplier applied to raw delta time before it is exposed as `DeltaTime` and `Now`. Set to values less than `1` for slow-motion, greater than `1` for fast-forward. Does not affect `UnscaledDeltaTime` or `NowUnscaled`.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
#### TimeTrackerDiagnoostics
```csharp
public static UpdateTimeTracker TimeTrackerDiagnoostics;
```

Only updated if [Game.DIAGNOSTICS_MODE](../Murder/Game.html#diagnostics_mode) is set.

**Returns** \
[UpdateTimeTracker](../Murder/Diagnostics/UpdateTimeTracker.html) \
#### UnscaledDeltaTime
```csharp
public static float UnscaledDeltaTime { get; }
```

De time difference between current and last update. Value is reliable only during the Update().

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
#### UpdateTime
```csharp
public float UpdateTime { get; private set; }
```

Wall-clock seconds the last `Update()` invocation consumed, including all ECS system updates. Compare against `DeltaTime` to detect performance bottlenecks.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
#### Width
```csharp
public static int Width { get; }
```

Gets the game width from the GameProfile. This is the intended size, not the actual size. For the current window size use [RenderContext.Camera](../Murder/Core/Graphics/RenderContext.html#camera).

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
#### Window
```csharp
public GameWindow Window { get; }
```

The MonoGame game window handle. Use to set the title (`Window.Title`), allow resizing (`Window.AllowUserResizing`), or listen to `ClientSizeChanged` events. Inherited from `Microsoft.Xna.Framework.Game`.

**Returns** \
[GameWindow](https://docs.monogame.net/api/Microsoft.Xna.Framework.GameWindow.html) \
### ⭐ Events
#### Activated
```csharp
public event EventHandler<TEventArgs> Activated;
```

Fired when the game window regains OS focus after being inactive. Use to resume audio, timers, or other focus-sensitive logic. Inherited from MonoGame.

**Returns** \
[EventHandler\<TEventArgs\>](https://learn.microsoft.com/en-us/dotnet/api/System.EventHandler-1?view=net-7.0) \
#### Deactivated
```csharp
public event EventHandler<TEventArgs> Deactivated;
```

Fired when the game window loses OS focus. Use to pause audio or lower frame-rate to conserve CPU. Inherited from MonoGame.

**Returns** \
[EventHandler\<TEventArgs\>](https://learn.microsoft.com/en-us/dotnet/api/System.EventHandler-1?view=net-7.0) \
#### Disposed
```csharp
public event EventHandler<TEventArgs> Disposed;
```

Fired when the game's `Dispose()` method completes. Useful for cleanup hooks that must run after the game's own disposal logic. Inherited from MonoGame.

**Returns** \
[EventHandler\<TEventArgs\>](https://learn.microsoft.com/en-us/dotnet/api/System.EventHandler-1?view=net-7.0) \
#### Exiting
```csharp
public event EventHandler<TEventArgs> Exiting;
```

Fired just before the game loop ends and the process exits. Subscribe to perform any last-moment cleanup or analytics flushing. Inherited from MonoGame.

**Returns** \
[EventHandler\<TEventArgs\>](https://learn.microsoft.com/en-us/dotnet/api/System.EventHandler-1?view=net-7.0) \
### ⭐ Methods
#### BeginDraw()
```csharp
protected virtual bool BeginDraw()
```

Called by MonoGame immediately before `Draw()`. Returns `false` to skip the current draw call. Overriding allows insertion of pre-draw logic or conditional suppression of rendering. Inherited from `Microsoft.Xna.Framework.Game`.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### ShowMissingRequirementMessage(Exception)
```csharp
protected virtual bool ShowMissingRequirementMessage(Exception exception)
```

Shows a platform-specific dialog when a required runtime dependency (e.g. a missing graphics feature) is absent. Returns `true` if the message was shown and the game should exit gracefully. Inherited from MonoGame.

**Parameters** \
`exception` [Exception](https://learn.microsoft.com/en-us/dotnet/api/System.Exception?view=net-7.0) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### LoadSceneAsync(bool)
```csharp
protected virtual Task LoadSceneAsync(bool waitForAllContent)
```

Asynchronously loads the game's content.

**Parameters** \
`waitForAllContent` [bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
\

**Returns** \
[Task](https://learn.microsoft.com/en-us/dotnet/api/System.Threading.Tasks.Task?view=net-7.0) \

#### ApplyGameSettingsImpl()
```csharp
protected virtual void ApplyGameSettingsImpl()
```

Virtual method for extended game settings application in derived classes.

#### BeginRun()
```csharp
protected virtual void BeginRun()
```

Called by MonoGame once, immediately before the main game loop starts. Override to perform one-time setup that must occur after `Initialize` and `LoadContent` but before the first `Update`. Inherited from `Microsoft.Xna.Framework.Game`.

#### Dispose(bool)
```csharp
protected virtual void Dispose(bool isDisposing)
```

Core disposal implementation. When `isDisposing` is `true`, managed resources (sound, data manager, scenes) are released. Call via `Dispose()` or the finalizer; do not call directly. Inherited pattern from `IDisposable`.

**Parameters** \
`isDisposing` [bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### Draw(GameTime)
```csharp
protected virtual void Draw(GameTime gameTime)
```

Renders the current frame, handling loading draw and ImGui rendering, and tracks rendering time.

**Parameters** \
`gameTime` [GameTime](https://docs.monogame.net/api/Microsoft.Xna.Framework.GameTime.html) \

#### DrawImGui(GameTime)
```csharp
protected virtual void DrawImGui(GameTime gameTime)
```

Placeholder for extending the ImGui drawing functionality in game editor.

**Parameters** \
`gameTime` [GameTime](https://docs.monogame.net/api/Microsoft.Xna.Framework.GameTime.html) \

#### EndDraw()
```csharp
protected virtual void EndDraw()
```

Called by MonoGame after `Draw()` completes. Presents the back buffer to the screen. Inherited from `Microsoft.Xna.Framework.Game`; override only if you need to insert post-present logic.

#### EndRun()
```csharp
protected virtual void EndRun()
```

Called by MonoGame after the main game loop exits. Override to add post-loop cleanup. Inherited from `Microsoft.Xna.Framework.Game`.

#### ExitGame()
```csharp
protected virtual void ExitGame()
```

Exit the game. This is used to wrap any custom behavior depending on the game implementation.

#### Finalize()
```csharp
protected virtual void Finalize()
```

#### Initialize()
```csharp
protected virtual void Initialize()
```

Initializes the game by setting up input bindings and configuring initial settings.
            Typically overridden by the game implementation.

#### LoadContent()
```csharp
protected virtual void LoadContent()
```

Loads game content and initializes it. This includes initializing the sound player, game data, settings, shaders, and initial scene. Also asynchronously loads the initial scene.

#### LoadContentImpl()
```csharp
protected virtual void LoadContentImpl()
```

Virtual method for extended content loading implementation in derived classes.

#### OnActivated(Object, EventArgs)
```csharp
protected virtual void OnActivated(Object sender, EventArgs args)
```

Raised when the game window gains focus. Fires the `Activated` event and may resume background operations. Inherited from MonoGame; override to add custom focus-gained behavior.

**Parameters** \
`sender` [Object](https://learn.microsoft.com/en-us/dotnet/api/System.Object?view=net-7.0) \
`args` [EventArgs](https://learn.microsoft.com/en-us/dotnet/api/System.EventArgs?view=net-7.0) \

#### OnDeactivated(Object, EventArgs)
```csharp
protected virtual void OnDeactivated(Object sender, EventArgs args)
```

Raised when the game window loses focus. Fires the `Deactivated` event. Override to pause audio or lower simulation fidelity when the player alt-tabs.

**Parameters** \
`sender` [Object](https://learn.microsoft.com/en-us/dotnet/api/System.Object?view=net-7.0) \
`args` [EventArgs](https://learn.microsoft.com/en-us/dotnet/api/System.EventArgs?view=net-7.0) \

#### OnExiting(Object, EventArgs)
```csharp
protected virtual void OnExiting(Object sender, EventArgs args)
```

Called by MonoGame just before the process exits. Murder uses this to call `IMurderGame.OnClose()`. Override to perform shutdown logic after the normal game teardown.

**Parameters** \
`sender` [Object](https://learn.microsoft.com/en-us/dotnet/api/System.Object?view=net-7.0) \
`args` [EventArgs](https://learn.microsoft.com/en-us/dotnet/api/System.EventArgs?view=net-7.0) \

#### OnLoadingDraw(RenderContext)
```csharp
protected virtual void OnLoadingDraw(RenderContext render)
```

Display drawing for the load animation.

**Parameters** \
`render` [RenderContext](../Murder/Core/Graphics/RenderContext.html) \

#### SetWindowSize(Point)
```csharp
protected virtual void SetWindowSize(Point screenSize)
```

Sets the window size for the game based on the specified screen size and full screen settings.

**Parameters** \
`screenSize` [Point](../Murder/Core/Geometry/Point.html) \
\

#### UnloadContent()
```csharp
protected virtual void UnloadContent()
```

Called by MonoGame to unload all managed content before the game exits. Override to release custom textures, audio, or other `IDisposable` assets that Murder does not own. Inherited from `Microsoft.Xna.Framework.Game`.

#### Update(GameTime)
```csharp
protected virtual void Update(GameTime gameTime)
```

Performs game frame updates, handling logic for paused states, fixed updates, and unscaled time.

**Parameters** \
`gameTime` [GameTime](https://docs.monogame.net/api/Microsoft.Xna.Framework.GameTime.html) \

#### ApplyGameSettings()
```csharp
protected void ApplyGameSettings()
```

Applies game settings based on the current [Murder.Game._gameData](). Configures grid and rendering settings, and calls an implementation-specific settings application method.

#### DoPendingExitGame()
```csharp
protected void DoPendingExitGame()
```

Executes the deferred exit logic set by `QueueExitGame()`. Called at the end of an update tick once `_pendingExit` is `true`, ensuring the world is not mid-update when disposal occurs.

#### DoPendingWorldTransition()
```csharp
protected void DoPendingWorldTransition()
```

Applies a pending world switch that was queued via `QueueWorldTransition` or `QueueReplaceWorldOnCurrentScene`. Swaps out the active world, optionally disposing the old one, and triggers the new world's start logic.

#### UpdateImpl(GameTime)
```csharp
protected void UpdateImpl(GameTime gameTime)
```

Implements core update logic, including frame freezing, world transitions, input handling, and time scaling.

**Parameters** \
`gameTime` [GameTime](https://docs.monogame.net/api/Microsoft.Xna.Framework.GameTime.html) \

#### CanResumeAfterSaveComplete()
```csharp
public bool CanResumeAfterSaveComplete()
```

Determines if the game can resume after a save operation is complete. Returns true if there's no active save data or the save operation has finished.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
\

#### QueueReplaceWorldOnCurrentScene(MonoWorld, bool)
```csharp
public bool QueueReplaceWorldOnCurrentScene(MonoWorld world, bool disposeWorld)
```

This is called when replacing the world for a current scene.
            Happened when transition from two different scenes (already loaded) as a world.

**Parameters** \
`world` [MonoWorld](../Murder/Core/MonoWorld.html) \
`disposeWorld` [bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### QueueWorldTransition(Guid)
```csharp
public bool QueueWorldTransition(Guid world)
```

Schedules a transition to the world asset identified by `world` (a `WorldAsset` GUID). The actual swap happens at the start of the next frame so the current update completes cleanly. Returns `true` if the transition was accepted.

**Parameters** \
`world` [Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### ResumeDeltaTimeOnUpdate()
```csharp
public bool ResumeDeltaTimeOnUpdate()
```

Resume game to normal game time.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### CreateRenderContext(GraphicsDevice, Camera2D, RenderContextFlags)
```csharp
public RenderContext CreateRenderContext(GraphicsDevice graphicsDevice, Camera2D camera, RenderContextFlags settings)
```

Creates a RenderContext using the specified graphics device, camera, and settings.
            Returns a new RenderContext if the game instance is null.
            Optionally implement this interface for using your custom RenderContext.

**Parameters** \
`graphicsDevice` [GraphicsDevice](https://docs.monogame.net/api/Microsoft.Xna.Framework.Graphics.GraphicsDevice.html) \
\
`camera` [Camera2D](../Murder/Core/Graphics/Camera2D.html) \
\
`settings` [RenderContextFlags](../Murder/Core/Graphics/RenderContextFlags.html) \
\

**Returns** \
[RenderContext](../Murder/Core/Graphics/RenderContext.html) \
\

#### BeginImGuiTheme()
```csharp
public virtual void BeginImGuiTheme()
```

Placeholder called before each ImGui draw pass. Override in an editor subclass (e.g. `Architect`) to push custom style colors and variables onto the ImGui style stack.

#### Dispose()
```csharp
public virtual void Dispose()
```

#### EndImGuiTheme()
```csharp
public virtual void EndImGuiTheme()
```

Called after each ImGui draw pass. Override alongside `BeginImGuiTheme()` to pop any custom style colors and variables from the ImGui style stack.

#### RefreshWindow()
```csharp
public virtual void RefreshWindow()
```

Refreshes the game window settings based on the current profile.

#### Exit()
```csharp
public void Exit()
```

Immediately signals MonoGame to stop the game loop and exit the process. Prefer `QueueExitGame()` over calling this directly to avoid disposing the world while it is actively being updated.

#### FreezeFrames(int)
```csharp
public void FreezeFrames(int amount)
```

This will pause the game for <paramref name="amount" /> of frames.

**Parameters** \
`amount` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### Pause()
```csharp
public void Pause()
```

This will pause the game.

#### QueueExitGame()
```csharp
public void QueueExitGame()
```

This queues such that the game exit at the end of the update.
            We wait until the end of the update to avoid any access to a world that has been disposed on cleanup.

#### ResetElapsedTime()
```csharp
public void ResetElapsedTime()
```

Resets the elapsed-time accumulator so the next frame receives a delta of zero. Useful after long loading pauses or debugging breaks to prevent a huge first-frame spike.

#### Resume()
```csharp
public void Resume()
```

This will resume the game.

#### Run()
```csharp
public void Run()
```

Starts the MonoGame event loop. Calls `Initialize`, `LoadContent`, then continuously calls `Update` and `Draw` until `Exit` is called. This is a blocking call — it returns only when the game closes.

#### RunOneFrame()
```csharp
public void RunOneFrame()
```

Advances the game by a single `Update`+`Draw` cycle. Used for unit tests or deterministic replay scenarios where the caller drives the game loop manually. Inherited from MonoGame.

#### SetWaitForSaveComplete()
```csharp
public void SetWaitForSaveComplete()
```

Sets the flag to indicate that the game should wait for the save operation to complete.

#### SkipDeltaTimeOnUpdate()
```csharp
public void SkipDeltaTimeOnUpdate()
```

This will skip update times and immediately run the update calls from the game 
            until [Game.ResumeDeltaTimeOnUpdate](../Murder/Game.html#resumedeltatimeonupdate) is called.

#### SuppressDraw()
```csharp
public void SuppressDraw()
```

Tells MonoGame to skip the `Draw` call for the current frame. Use when the scene state hasn't changed and redrawing would be wasteful. Inherited from `Microsoft.Xna.Framework.Game`.

#### Tick()
```csharp
public void Tick()
```

Manually ticks one frame of the game loop (equivalent to a single `Update`+`Draw` step). Intended for headless testing or tooling scenarios where you control the loop. Inherited from MonoGame.



⚡