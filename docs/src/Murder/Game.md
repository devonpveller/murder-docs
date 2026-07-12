# Game

**Namespace:** Murder \
**Assembly:** Murder.dll

```csharp
public partial class Game : Microsoft.Xna.Framework.Game
```

**Implements:** _[Game](https://docs.monogame.net/api/Microsoft.Xna.Framework.Game.html), [IDisposable](https://learn.microsoft.com/en-us/dotnet/api/System.IDisposable?view=net-7.0)_

**Intent:** `Game` is the singleton root of the Murder engine. It is a `partial class` split across `Game.cs` (the main loop, timing, window management) and `Game_Scenes.cs` (queued world/scene transitions and exit). It owns the MonoGame/FNA game loop, the active scene/world (via its internal `SceneLoader`), all timing state, and top-level subsystem references (input, sound, haptics, data, graphics). Every game built on Murder instantiates exactly one `Game` (or a derived subclass, such as the editor's `Architect`).

**Use-case:** Implement [IMurderGame](../Murder/IMurderGame.html) with your game-specific logic, construct `Game` with it, and call `Run()`. Access global engine state via static helpers such as `Game.Data`, `Game.Input`, `Game.Sound`, `Game.Now`, and `Game.Profile`. To switch levels call `QueueWorldTransition(Guid)`. Pause/resume timing with `Pause()` / `Resume()`. Use `FreezeFrames(n)` for screen-shake or hit-stop effects. Most day-to-day game code interacts with `Game` only through its static accessors rather than by holding a reference to the instance itself.

### ⭐ Constructors

```csharp
public Game(IMurderGame? game, GameDataManager dataManager)
```

Creates a new game; there should only ever be one `Game` instance. Wires up the window-resize handler, mouse-cursor visibility (from `HasCursor`/`IMurderGame.HasCursor`), the logger, `PlayerInput`, the sound player (via `IMurderGame.CreateSoundPlayer`), `Haptics`, the `GraphicsDeviceManager`, and an optional preload screen (via `TryCreatePreloadScreen`). Use the other constructor overload unless you need to supply a pre-built `GameDataManager`.

**Parameters** \
`game` [IMurderGame](../Murder/IMurderGame.html) \
`dataManager` [GameDataManager](../Murder/Data/GameDataManager.html) \

```csharp
public Game(IMurderGame? game = null)
```

Convenience overload that builds a fresh `GameDataManager` for `game` and delegates to the primary constructor. This is the constructor almost every game should call — typically from its `Main` entry point as `new Game(new MyGame()).Run()`. `game` may be `null` for minimal/headless setups that don't need any `IMurderGame` callbacks.

**Parameters** \
`game` [IMurderGame](../Murder/IMurderGame.html) \

### ⭐ Properties

#### \_disposePendingWorld

```csharp
protected bool _disposePendingWorld;
```

When `true`, the world stored in `_pendingWorld` will be disposed (rather than recycled) once it is replaced by the next pending world. Set via `QueueReplaceWorldOnCurrentScene(MonoWorld, bool)`.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### \_gameData

```csharp
protected readonly GameDataManager _gameData;
```

The central asset and save-data manager for this game instance. Accessible publicly via the static `Game.Data` shortcut.

**Returns** \
[GameDataManager](../Murder/Data/GameDataManager.html) \

#### \_game

```csharp
protected readonly IMurderGame? _game;
```

The `IMurderGame` implementation supplied to the constructor. All lifecycle callbacks and factory methods on `Game` delegate to this instance when it is non-null. Accessible publicly (read-only) via the `MurderGame` property.

**Returns** \
[IMurderGame](../Murder/IMurderGame.html) \

#### \_graphics

```csharp
protected readonly GraphicsDeviceManager _graphics;
```

MonoGame's `GraphicsDeviceManager` used to configure resolution, fullscreen mode, and V-sync. Exposed publicly via the `GraphicsDeviceManager` property and statically via `Game.GraphicsDevice`.

**Returns** \
[GraphicsDeviceManager](https://docs.monogame.net/api/Microsoft.Xna.Framework.GraphicsDeviceManager.html) \

#### \_logger

```csharp
protected GameLogger _logger;
```

Single logger of the game.

**Returns** \
[GameLogger](../Murder/Diagnostics/GameLogger.html) \

#### \_pendingExit

```csharp
protected bool _pendingExit;
```

Set to `true` by `QueueExitGame()`. The game loop checks this flag at the end of each update and calls `ExitGame()` safely, avoiding disposal of a world that is mid-update.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### \_pendingResetSave

```csharp
protected bool _pendingResetSave;
```

When `true`, the active save data is discarded (`GameDataManager.ResetActiveSave`) as part of applying the pending world transition. Set by `QueueWorldTransition(Guid, bool)`.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### \_pendingWorld

```csharp
protected MonoWorld? _pendingWorld;
```

A fully-initialized `MonoWorld` that is waiting to replace the current active world at the start of the next frame. Populated by `QueueReplaceWorldOnCurrentScene`.

**Returns** \
[MonoWorld](../Murder/Core/MonoWorld.html) \

#### \_pendingWorldTransition

```csharp
protected Guid? _pendingWorldTransition;
```

GUID of the `WorldAsset` queued by `QueueWorldTransition(Guid)`, waiting to be applied by `DoPendingWorldTransition` at the start of the next update. `null` when no full scene transition is pending.

**Returns** \
[Guid?](https://learn.microsoft.com/en-us/dotnet/api/System.Nullable-1?view=net-7.0) \

#### \_playerInput

```csharp
protected readonly PlayerInput _playerInput;
```

The engine-wide input manager that tracks keyboard, mouse, and gamepad state. Accessible via the static `Game.Input` shortcut.

**Returns** \
[PlayerInput](../Murder/Core/Input/PlayerInput.html) \

#### \_sceneLoader

```csharp
protected SceneLoader? _sceneLoader;
```

Initialized in [Game.LoadContent](../Murder/Game.html#loadcontent). Drives the active `Scene`/`MonoWorld`; `ActiveScene` reads through this.

**Returns** \
[SceneLoader](../Murder/Core/SceneLoader.html) \

#### ActiveScene

```csharp
public Scene? ActiveScene { get; }
```

The currently loaded `Scene`, sourced from `_sceneLoader`. `null` until `LoadContent` has created the `SceneLoader` and it has loaded a scene. Most systems reach the active world through `Game.Instance.ActiveScene` or, more commonly, through the `World` they already belong to.

**Returns** \
[Scene](../Murder/Core/Scene.html) \

#### CanSave

```csharp
public static bool CanSave { get; }
```

Whether the game supports saving progress, sourced from `IMurderGame.CanSave` (defaults to `false` if there is no `IMurderGame` implementation). Check this before showing save/load UI.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### Components

```csharp
public GameComponentCollection Components { get; }
```

MonoGame's collection of `IGameComponent` objects that receive automatic `Initialize`, `Update`, and `Draw` calls. Rarely used directly in Murder; prefer ECS systems instead. Inherited from `Microsoft.Xna.Framework.Game`.

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

Gets the `GameDataManager` instance.

**Returns** \
[GameDataManager](../Murder/Data/GameDataManager.html) \

#### DefaultHeight

```csharp
public static int DefaultHeight { get; }
```

Gets the design-time game height, sourced from `IMurderGame.GameHeight` (or `180` if there is no `IMurderGame` implementation). This is the intended size, not the actual size. For the current window size use [RenderContext.Camera](../Murder/Core/Graphics/RenderContext.html#camera).

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### DefaultScale

```csharp
public static float DefaultScale { get; }
```

Gets the design-time pixel scale, sourced from `IMurderGame.Scale` (or `2` if there is no `IMurderGame` implementation). Used together with `DefaultWidth`/`DefaultHeight` to compute the initial window size in `FlushWindow`.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### DefaultWidth

```csharp
public static int DefaultWidth { get; }
```

Gets the design-time game width, sourced from `IMurderGame.GameWidth` (or `320` if there is no `IMurderGame` implementation). This is the intended size, not the actual size. For the current window size use [RenderContext.Camera](../Murder/Core/Graphics/RenderContext.html#camera).

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### DeltaTime

```csharp
public static float DeltaTime { get; }
```

The time difference between the current and last update, scaled by pause state and `TimeScale`. Value is reliable only during `Update()`; it is zero during render.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### DIAGNOSTICS_MODE

```csharp
public static bool DIAGNOSTICS_MODE;
```

Use this to set whether diagnostics should be pulled. When `true`, `Game` measures and tracks per-frame `UpdateTime`, `RenderTime`, `ImGuiRenderTime`, and `SoundUpdateTime`, and feeds `TimeTrackerDiagnostics`/`RenderTimeTrackerDiagnostics`. Defaults to `true`.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### Downsample

```csharp
public float Downsample;
```

Render-resolution scaling factor. A value of `1` renders at full resolution; values below `1` render to a smaller target and upscale, improving performance at the cost of quality.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### FeedbackUrl

```csharp
public static string FeedbackUrl { get; }
```

Gets the URL to report bugs or feedback, sourced from `IMurderGame.FeedbackUrl` (or an empty string if there is no `IMurderGame` implementation). Editor and crash-report UI use this to point players/testers at the right place.

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### FixedDeltaTime

```csharp
public static float FixedDeltaTime { get; }
```

Gets the fixed delta time in seconds, derived from `GameProfile.TargetFps` (`1f / fixedFps`). This is the step size used by fixed updates in `UpdateImpl`.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### FixedNow

```csharp
public static float FixedNow { get; }
```

Gets the scaled time (in seconds since the game started) at which the last fixed update ran. Unlike `Now`, which advances every frame, this only advances in `FixedDeltaTime` increments inside `UpdateImpl`, making it the right clock to read from physics or other fixed-step systems.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### Fullscreen

```csharp
public bool Fullscreen { get; public set; }
```

Gets or sets the fullscreen mode of the game, backed by `Preferences.Fullscreen`. Setting it queues a window change (via `OnWindowChange`) and persists the new preference; it is a no-op if the value doesn't actually change.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### GameScale

```csharp
public Vector2 GameScale { get; }
```

Gets the scale of the current window relative to the internal render resolution (`_screenSize`) and `DefaultScale`. Returns `Vector2.One` if the window or internal screen size is invalid/zero. Used by rendering/UI code that needs to map between window pixels and design-resolution pixels.

**Returns** \
[Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

#### GraphicsDevice

```csharp
public static GraphicsDevice GraphicsDevice { get; }
```

Gets the current instance of the `GraphicsDevice`, sourced from `_graphics`.

**Returns** \
[GraphicsDevice](https://docs.monogame.net/api/Microsoft.Xna.Framework.Graphics.GraphicsDevice.html) \

#### GraphicsDeviceManager

```csharp
public GraphicsDeviceManager GraphicsDeviceManager { get; }
```

Public accessor for the `_graphics` field. Use this to query or change graphics settings such as preferred back-buffer dimensions, V-sync, or fullscreen state.

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

Beautiful hardcoded grid so it's very easy to access in game! Rebuilt from `GameProfile.DefaultGridCellSize` in `ApplyGameSettings`; used by grid-based gameplay/collision systems.

**Returns** \
[GridConfiguration](../Murder/Core/GridConfiguration.html) \

#### Haptics

```csharp
public readonly HapticsManager Haptics;
```

Manages gamepad rumble/vibration effects for this game instance. Systems that want to trigger controller haptics (e.g. on hit or explosion) should go through this instance rather than talking to the gamepad API directly, since it tracks and clears active effects on scene close.

**Returns** \
[HapticsManager](../Murder/Core/Input/HapticsManager.html) \

#### HasCursor

```csharp
public virtual bool HasCursor { get; }
```

Whether this game renders a visible cursor. Combined with `IMurderGame.HasCursor` in the constructor to set `IsMouseVisible`. Defaults to `false` in the base `Game`; override in a subclass (such as the editor) if cursor visibility should depend on engine-level state rather than the `IMurderGame` implementation.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

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

The first `Scene` the engine creates when the game starts: `new GameScene(Profile.StartingScene)`. Override in a subclass to launch with a different or custom scene.

**Returns** \
[Scene](../Murder/Core/Scene.html) \

#### Input

```csharp
public static PlayerInput Input { get; }
```

Gets the `PlayerInput` instance.

**Returns** \
[PlayerInput](../Murder/Core/Input/PlayerInput.html) \

#### Instance

```csharp
public static Game Instance { get; private set; }
```

Singleton instance of the game. Set the moment the constructor runs. Be cautious when referencing this from code that could run before the constructor finishes or after `Dispose`.

**Returns** \
[Game](../Murder/Game.html) \

#### IsActive

```csharp
public bool IsActive { get; internal set; }
```

`true` while the game window has OS focus. Inherited from `Microsoft.Xna.Framework.Game`; when `false` the game may sleep for `InactiveSleepTime` per frame.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### IsDiagnosticEnabled

```csharp
protected virtual bool IsDiagnosticEnabled { get; }
```

Whether the in-game diagnostic overlay is active. Defaults to `false`; the editor (`Architect`) overrides this to `true`. Passed to `GameLogger.Initialize` and the `SceneLoader`.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### IsFixedTimeStep

```csharp
public bool IsFixedTimeStep { get; public set; }
```

When `true`, MonoGame attempts to call `Update` at a steady rate driven by V-sync. `ApplyGameSettings` sets this to `true`. Inherited from `Microsoft.Xna.Framework.Game`; Murder's own fixed-step accumulation in `UpdateImpl` is independent of this flag.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### IsMouseVisible

```csharp
public bool IsMouseVisible { get; public set; }
```

Controls OS-level mouse cursor visibility. Murder sets this from `HasCursor`/`IMurderGame.HasCursor` in the constructor. Inherited from `Microsoft.Xna.Framework.Game`.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### IsPaused

```csharp
public bool IsPaused { get; private set; }
```

`true` when the game has been paused via `Pause()`. While paused, scaled time (`DeltaTime`/`Now`) does not advance. Resume normal play with `Resume()`.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### IsSkippingDeltaTimeOnUpdate

```csharp
public bool IsSkippingDeltaTimeOnUpdate { get; }
```

Whether the player is currently skipping frames (e.g. fast-forwarding through a cutscene) and update calls are running with a fixed step, ignoring real elapsed time. Set via `SkipDeltaTimeOnUpdate()` / cleared via `ResumeDeltaTimeOnUpdate()`.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### LaunchParameters

```csharp
public LaunchParameters LaunchParameters { get; }
```

Command-line arguments parsed by MonoGame at startup. Use to implement launch flags such as `-fullscreen`. Inherited from `Microsoft.Xna.Framework.Game`.

**Returns** \
[LaunchParameters](https://docs.monogame.net/api/Microsoft.Xna.Framework.LaunchParameters.html) \

#### LONGEST_TIME_RESET

```csharp
public const float LONGEST_TIME_RESET = 5f;
```

The number of seconds after which `LongestUpdateTime` and `LongestRenderTime` are automatically reset. Prevents stale spikes from dominating the diagnostic display indefinitely.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### LongestRenderTime

```csharp
public float LongestRenderTime { get; private set; }
```

Gets the longest `RenderTime` recorded since the last `LONGEST_TIME_RESET` interval. Only tracked while `DIAGNOSTICS_MODE` is set.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### LongestUpdateTime

```csharp
public float LongestUpdateTime { get; private set; }
```

The largest `UpdateTime` value recorded since the last `LONGEST_TIME_RESET` interval. Only tracked while `DIAGNOSTICS_MODE` is set. Useful for identifying frame spikes in diagnostics.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### LoosingFrames

```csharp
public static bool LoosingFrames { get; private set; }
```

Set to `true` when `UpdateImpl` hits the per-frame cap of fixed updates and has to drop the accumulated remainder instead of catching up. Indicates the simulation cannot keep up with real time; use it to detect sustained performance problems.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### MaxDeltaTime

```csharp
public static float MaxDeltaTime { get; set; }
```

Diagnostic high-water mark of the largest raw frame delta observed by `Update`. Not reset automatically; useful for spotting stalls or hitches over a session.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### MaxFixedUpdatesInASingleFrame

```csharp
public static int MaxFixedUpdatesInASingleFrame { get; set; }
```

Diagnostic high-water mark of how many fixed-update steps were run within a single frame. Not reset automatically; useful for spotting frames that required catch-up simulation.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### MurderGame

```csharp
public IMurderGame? MurderGame { get; }
```

Public accessor for the `IMurderGame` implementation passed into the constructor (`_game`). Useful for systems and editor tooling that need to reach game-specific callbacks or metadata (such as `IMurderGame.Name`) without depending on a concrete subclass of `Game`.

**Returns** \
[IMurderGame](../Murder/IMurderGame.html) \

#### Now

```csharp
public static float Now { get; }
```

Gets the current scaled elapsed time (seconds since the game started, affected by `TimeScale` and pause).

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### NowUnscaled

```csharp
public static float NowUnscaled { get; }
```

Gets the current unscaled elapsed time (seconds since the game started, not affected by `TimeScale` or pause).

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### Preferences

```csharp
public static GamePreferences Preferences { get; }
```

Gets the `GamePreferences` asset instance.

**Returns** \
[GamePreferences](../Murder/Save/GamePreferences.html) \

#### PreviousElapsedTime

```csharp
public float PreviousElapsedTime { get; }
```

Elapsed (scaled) time in seconds from the previous fixed update, since the game started.

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

Time from the previous fixed update, unscaled.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### Profile

```csharp
public static GameProfile Profile { get; }
```

Gets the `GameProfile` asset instance.

**Returns** \
[GameProfile](../Murder/Assets/GameProfile.html) \

#### Random

```csharp
public static Random Random;
```

Provides a static `Random` instance shared across the engine. Prefer this over creating your own `Random` when determinism/seeding is not a concern, so debugging tools (e.g. `SimulateRandomStalls`) share the same source.

**Returns** \
[Random](https://learn.microsoft.com/en-us/dotnet/api/System.Random?view=net-7.0) \

#### RenderTime

```csharp
public float RenderTime { get; private set; }
```

Time in seconds that the `Draw()` method took to finish.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### RenderTimeTrackerDiagnostics

```csharp
public static UpdateTimeTracker RenderTimeTrackerDiagnostics;
```

Only updated if [Game.DIAGNOSTICS_MODE](../Murder/Game.html#diagnostics_mode) is set. Tracks a rolling history of `RenderTime` samples for diagnostics overlays/graphs.

**Returns** \
[UpdateTimeTracker](../Murder/Diagnostics/UpdateTimeTracker.html) \

#### Save

```csharp
public static SaveData Save { get; }
```

Gets the active `SaveData` asset instance.

**Returns** \
[SaveData](../Murder/Assets/SaveData.html) \

#### ScreenSize

```csharp
public Point ScreenSize { get; }
```

Raw size, in pixels, of the internal render target/screen, as last applied by `FlushWindow`. Distinct from `GetWindowSize()`, which returns the actual OS window size (they differ, for example, when `Downsample` is not `1`).

**Returns** \
[Point](../Murder/Core/Geometry/Point.html) \

#### Services

```csharp
public GameServiceContainer Services { get; }
```

MonoGame's service-locator container for sharing objects between game components. Murder uses its own dependency-injection patterns (static accessors, `Game.Data`, etc.); this is primarily an inherited MonoGame surface.

**Returns** \
[GameServiceContainer](https://docs.monogame.net/api/Microsoft.Xna.Framework.GameServiceContainer.html) \

#### SlowdownDetected

```csharp
public static bool SlowdownDetected { get; private set; }
```

Set every fixed step inside `UpdateImpl` when the incoming frame delta is more than 1.5x `FixedDeltaTime`, i.e. the game is running noticeably behind its target framerate. Useful for diagnostics overlays that want to flag slow frames without tracking raw timings themselves.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### Sound

```csharp
public static ISoundPlayer Sound { get; }
```

Gets the `ISoundPlayer` instance.

**Returns** \
[ISoundPlayer](../Murder/Core/Sounds/ISoundPlayer.html) \

#### SoundPlayer

```csharp
public readonly ISoundPlayer SoundPlayer;
```

The concrete sound subsystem instance for this game, created from `IMurderGame.CreateSoundPlayer` (or a default `SoundPlayer` if there is no `IMurderGame` implementation). Access it globally via the `Game.Sound` static shortcut.

**Returns** \
[ISoundPlayer](../Murder/Core/Sounds/ISoundPlayer.html) \

#### SoundUpdateTime

```csharp
public float SoundUpdateTime { get; private set; }
```

Time in seconds that `ISoundPlayer.Update` and `HapticsManager.Update` took to finish during the last `Update` call. Only measured while `DIAGNOSTICS_MODE` is set.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### StartedSkippingCutscene

```csharp
public bool StartedSkippingCutscene;
```

Whether the player started skipping. Reset to `false` whenever `SkipDeltaTimeOnUpdate()` is called; set to `true` by game-specific code driving a cutscene-skip.

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

#### TimeTrackerDiagnostics

```csharp
public static UpdateTimeTracker TimeTrackerDiagnostics;
```

Only updated if [Game.DIAGNOSTICS_MODE](../Murder/Game.html#diagnostics_mode) is set. Tracks a rolling history of `UpdateTime` samples for diagnostics overlays/graphs.

**Returns** \
[UpdateTimeTracker](../Murder/Diagnostics/UpdateTimeTracker.html) \

#### UnscaledDeltaTime

```csharp
public static float UnscaledDeltaTime { get; }
```

The time difference between the current and last update, not scaled by pause or `TimeScale`. Value is reliable only during `Update()`.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### UpdateTime

```csharp
public float UpdateTime { get; private set; }
```

Time in seconds that the `Update()` methods took to finish. This is not the time between updates (that's `DeltaTime`); it is the time the systems actually take to update the game logic, including all systems, components, and render systems.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### UseXnaGameTime

```csharp
public static bool UseXnaGameTime { get; set; }
```

Reserved flag for toggling between XNA's `GameTime`-based timing and an alternative timing source. Currently informational only — the engine's own update loop always derives its clocks from `GameTime`. Defaults to `true`.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### Window

```csharp
public GameWindow Window { get; }
```

The MonoGame game window handle. Use to set the title (`Window.Title`), allow resizing (`Window.AllowUserResizing`, enabled by default in the constructor), or listen to `ClientSizeChanged` events. Inherited from `Microsoft.Xna.Framework.Game`.

**Returns** \
[GameWindow](https://docs.monogame.net/api/Microsoft.Xna.Framework.GameWindow.html) \

### ⭐ Events

#### Activated

```csharp
public event EventHandler<TEventArgs> Activated;
```

Fired when the game window regains OS focus after being inactive. Inherited from MonoGame.

**Returns** \
[EventHandler\<TEventArgs\>](https://learn.microsoft.com/en-us/dotnet/api/System.EventHandler-1?view=net-7.0) \

#### Deactivated

```csharp
public event EventHandler<TEventArgs> Deactivated;
```

Fired when the game window loses OS focus. Inherited from MonoGame.

**Returns** \
[EventHandler\<TEventArgs\>](https://learn.microsoft.com/en-us/dotnet/api/System.EventHandler-1?view=net-7.0) \

#### Disposed

```csharp
public event EventHandler<TEventArgs> Disposed;
```

Fired when the game's `Dispose()` method completes. Inherited from MonoGame.

**Returns** \
[EventHandler\<TEventArgs\>](https://learn.microsoft.com/en-us/dotnet/api/System.EventHandler-1?view=net-7.0) \

#### Exiting

```csharp
public event EventHandler<TEventArgs> Exiting;
```

Fired just before the game loop ends and the process exits. Inherited from MonoGame; `Game` overrides `OnExiting` (which raises this event) to log a shutdown message.

**Returns** \
[EventHandler\<TEventArgs\>](https://learn.microsoft.com/en-us/dotnet/api/System.EventHandler-1?view=net-7.0) \

### ⭐ Methods

#### BeginDraw()

```csharp
protected virtual bool BeginDraw()
```

Called by MonoGame immediately before `Draw()`. Returns `false` to skip the current draw call. Inherited from `Microsoft.Xna.Framework.Game`; not overridden by Murder.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### ShowMissingRequirementMessage(Exception)

```csharp
protected virtual bool ShowMissingRequirementMessage(Exception exception)
```

Shows a platform-specific dialog when a required runtime dependency (e.g. a missing graphics feature) is absent. Inherited from `Microsoft.Xna.Framework.Game`; not overridden by Murder.

**Parameters** \
`exception` [Exception](https://learn.microsoft.com/en-us/dotnet/api/System.Exception?view=net-7.0) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### LoadSceneAsync(Boolean)

```csharp
protected virtual Task LoadSceneAsync(bool waitForAllContent)
```

Waits for any in-flight content loading (`GameDataManager.LoadContentProgress`), calls `IMurderGame.LoadContentAsync` followed by `IMurderGame.OnSceneTransition`, then tells the `SceneLoader` to load its content. Called from `LoadContent` on startup and again from `DoPendingWorldTransition` after every world/scene transition. Any exception is logged, captured as a crash, and results in `ExitGame()`.

**Parameters** \
`waitForAllContent` [bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

**Returns** \
[Task](https://learn.microsoft.com/en-us/dotnet/api/System.Threading.Tasks.Task?view=net-7.0) \

#### TryCreatePreloadScreen()

```csharp
protected virtual IPreloadGame? TryCreatePreloadScreen()
```

Creates the optional preload screen shown while the game's initial content is still loading, by delegating to `IMurderGame.TryCreatePreload`. Returns `null` if there is no `IMurderGame` implementation or it does not provide one. Override to force a different preload behavior regardless of what `IMurderGame` returns.

**Returns** \
[IPreloadGame](../Murder/Core/IPreloadGame.html) \

#### ApplyGameSettingsImpl()

```csharp
protected virtual void ApplyGameSettingsImpl()
```

Virtual method for extended game settings application in derived classes. Called at the end of `ApplyGameSettings()`.

#### BeginRun()

```csharp
protected virtual void BeginRun()
```

Called by MonoGame once, immediately before the main game loop starts. Inherited from `Microsoft.Xna.Framework.Game`; not overridden by Murder.

#### Dispose(Boolean)

```csharp
protected virtual void Dispose(bool isDisposing)
```

Core disposal implementation. Stops any playing media (`MediaPlayer.Stop()`), disposes `ActiveScene` and `Data`, then calls `base.Dispose(isDisposing)`. Called via `Dispose()` or the finalizer; do not call directly.

**Parameters** \
`isDisposing` [bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### Draw(GameTime)

```csharp
protected virtual void Draw(GameTime gameTime)
```

Renders the current frame: flushes any pending window change, draws the preload/loading screen via `OnLoadingDraw` if content isn't ready yet, otherwise draws the active scene (`DrawScene`), calls `base.Draw`, then `DrawImGui`. Tracks `RenderTime`/`ImGuiRenderTime`/`LongestRenderTime` while `DIAGNOSTICS_MODE` is set, and calls `IMurderGame.AfterDraw` at the end.

**Parameters** \
`gameTime` [GameTime](https://docs.monogame.net/api/Microsoft.Xna.Framework.GameTime.html) \

#### DrawImGui(GameTime)

```csharp
protected virtual void DrawImGui(GameTime gameTime)
```

Placeholder for extending the ImGui drawing functionality in game editor. Empty in the base `Game`; the editor's `Architect` overrides this to draw its ImGui panels.

**Parameters** \
`gameTime` [GameTime](https://docs.monogame.net/api/Microsoft.Xna.Framework.GameTime.html) \

#### EndDraw()

```csharp
protected virtual void EndDraw()
```

Called by MonoGame after `Draw()` completes; presents the back buffer to the screen. Inherited from `Microsoft.Xna.Framework.Game`; not overridden by Murder.

#### EndRun()

```csharp
protected virtual void EndRun()
```

Called by MonoGame after the main game loop exits. Inherited from `Microsoft.Xna.Framework.Game`; not overridden by Murder.

#### ExitGame()

```csharp
protected virtual void ExitGame()
```

Exit the game. This is used to wrap any custom behavior depending on the game implementation; the base implementation simply calls `base.Exit()`. Invoked from `DoPendingExitGame()` (queued path) or directly when `LoadSceneAsync` fails.

#### Finalize()

```csharp
protected virtual void Finalize()
```

Standard .NET finalizer, inherited via the `IDisposable`/`Dispose(bool)` pattern from `Microsoft.Xna.Framework.Game`. Not overridden by Murder; do not call directly.

#### FlushWindow()

```csharp
protected virtual void FlushWindow()
```

Applies a pending window change queued via `OnWindowChange` (or set directly during construction/`Fullscreen`): computes the target size for the requested `ScreenUpdatedKind` (full screen uses the display size, `Reset` uses `DefaultWidth`/`DefaultHeight`/`DefaultScale` with a fallback to a smaller scale if it wouldn't fit the display), applies it via `SetWindowSizeAndApply`, updates `_screenSize`/`ScreenSize`, and notifies `ActiveScene.OnClientWindowChanged`. Called from `Initialize()` at startup and from `Draw()` whenever a change is pending.

#### Initialize()

```csharp
protected virtual void Initialize()
```

Initializes the game by registering the component lookup (`World.InitializeLookupComponents`), subscribing `OnClose` to `AppDomain.ProcessExit`, registering the built-in editor/navigation input buttons and axes on `_playerInput`, calling `base.Initialize()` (which loads content), then `IMurderGame.Initialize()`, propagating `DIAGNOSTICS_MODE` to `World`, starting the internal wall-clock stopwatch, and flushing any pending window change. Typically not overridden directly by games — use `IMurderGame.Initialize` instead.

#### LoadContent()

```csharp
protected virtual void LoadContent()
```

Loads game content and initializes it: initializes the sound player, initializes `_gameData`, applies game settings (`ApplyGameSettings`), sets the target fixed framerate from `Profile.TargetFps`, runs `LoadContentImpl()`, loads shaders (including any `IShaderProvider` custom shaders), loads all other content via `_gameData.LoadContent()`, creates the `SceneLoader` for `InitialScene`, and kicks off `LoadSceneAsync(waitForAllContent: true)`.

#### LoadContentImpl()

```csharp
protected virtual void LoadContentImpl()
```

Virtual method for extended content loading implementation in derived classes. Called from `LoadContent()`, before shaders/content are loaded.

#### OnActivated(Object, EventArgs)

```csharp
protected virtual void OnActivated(Object sender, EventArgs args)
```

Raised when the game window gains focus; fires the `Activated` event. Inherited from `Microsoft.Xna.Framework.Game`; not overridden by Murder.

**Parameters** \
`sender` [Object](https://learn.microsoft.com/en-us/dotnet/api/System.Object?view=net-7.0) \
`args` [EventArgs](https://learn.microsoft.com/en-us/dotnet/api/System.EventArgs?view=net-7.0) \

#### OnClose(Object, EventArgs)

```csharp
protected virtual void OnClose(Object? sender, EventArgs e)
```

Handler subscribed to `AppDomain.ProcessExit` in `Initialize()`. Runs on regular process shutdown — unlike `OnExiting`, which only fires when `Exit()` is called through the MonoGame loop — so it also covers the game being killed externally or the OS closing the window. Delegates to `OnCloseImpl()`.

**Parameters** \
`sender` [Object](https://learn.microsoft.com/en-us/dotnet/api/System.Object?view=net-7.0) \
`e` [EventArgs](https://learn.microsoft.com/en-us/dotnet/api/System.EventArgs?view=net-7.0) \

#### OnCloseImpl()

```csharp
protected virtual void OnCloseImpl()
```

Shared shutdown logic invoked from both `OnClose` and `OnUnhandledException`. Clears any active haptics/rumble effects (`Haptics.ClearAll()`) and calls `IMurderGame.OnClose()` so the game can flush preferences, analytics, or other state right before the process actually terminates.

#### OnDeactivated(Object, EventArgs)

```csharp
protected virtual void OnDeactivated(Object sender, EventArgs args)
```

Raised when the game window loses focus; fires the `Deactivated` event. Inherited from `Microsoft.Xna.Framework.Game`; not overridden by Murder.

**Parameters** \
`sender` [Object](https://learn.microsoft.com/en-us/dotnet/api/System.Object?view=net-7.0) \
`args` [EventArgs](https://learn.microsoft.com/en-us/dotnet/api/System.EventArgs?view=net-7.0) \

#### OnExiting(Object, EventArgs)

```csharp
protected override void OnExiting(Object sender, EventArgs args)
```

Called by MonoGame just before the process exits (only when the shutdown goes through `Exit()`). Murder's override simply logs a shutdown message; it does **not** call `IMurderGame.OnClose()` — that happens separately via `OnClose`/`OnCloseImpl`, which is wired to `AppDomain.ProcessExit` so it also fires on external process termination.

**Parameters** \
`sender` [Object](https://learn.microsoft.com/en-us/dotnet/api/System.Object?view=net-7.0) \
`args` [EventArgs](https://learn.microsoft.com/en-us/dotnet/api/System.EventArgs?view=net-7.0) \

#### OnLoadingDraw(RenderContext)

```csharp
protected virtual void OnLoadingDraw(RenderContext render)
```

Display drawing for the load animation. If a preload screen is active (`_preload`), delegates to its `Draw`; otherwise clears the render target. Called from `Draw()` whenever content isn't fully loaded yet.

**Parameters** \
`render` [RenderContext](../Murder/Core/Graphics/RenderContext.html) \

#### SetWindowSizeAndApply(Point)

```csharp
protected virtual void SetWindowSizeAndApply(Point screenSize)
```

Applies the given screen size to the OS window and `GraphicsDeviceManager`. In fullscreen, remembers the previous windowed size, makes the window borderless, and sets `_graphics.IsFullScreen = true`; otherwise sets a bordered, non-fullscreen window with the given back-buffer dimensions. Calls `_graphics.ApplyChanges()`. Called from `FlushWindow`; renamed from the older `SetWindowSize`.

**Parameters** \
`screenSize` [Point](../Murder/Core/Geometry/Point.html) \

#### UnloadContent()

```csharp
protected virtual void UnloadContent()
```

Called by MonoGame to unload all managed content before the game exits. Inherited from `Microsoft.Xna.Framework.Game`; not overridden by Murder — override in a subclass to release custom textures, audio, or other `IDisposable` assets the engine does not own.

#### Update(GameTime)

```csharp
protected virtual void Update(GameTime gameTime)
```

Performs game frame updates: updates the preload screen if any, tracks `UpdateTime` diagnostics, waits (without simulating) while a save is in-flight (`_waitForSaveComplete`), fires `GameDataManager.AfterContentLoadedFromMainThread` once loading finishes, calls `UpdateImpl` with the delta time clamped to at most `FixedDeltaTime * 3` (to avoid spiral-of-death catch-up), repeats `UpdateImpl(FixedDeltaTime)` while `IsSkippingDeltaTimeOnUpdate` is set (cutscene skip), and finally updates `SoundPlayer` and `Haptics`.

**Parameters** \
`gameTime` [GameTime](https://docs.monogame.net/api/Microsoft.Xna.Framework.GameTime.html) \

#### ApplyGameSettings()

```csharp
protected void ApplyGameSettings()
```

Applies game settings based on the current `Profile`: rebuilds `Grid` from `Profile.DefaultGridCellSize`, syncs V-sync (`_graphics.SynchronizeWithVerticalRetrace`) with `Profile.IsVSyncEnabled`, sets `IsFixedTimeStep = true`, calls `ApplyGameSettingsImpl()`, and applies the graphics changes.

#### DoPendingExitGame()

```csharp
protected void DoPendingExitGame()
```

Executes the deferred exit requested via `QueueExitGame()`, if any, by calling `ExitGame()`. Called once per frame from `UpdateImpl` so the world is never disposed while it is mid-update.

#### DoPendingWorldTransition()

```csharp
protected void DoPendingWorldTransition()
```

Applies whichever world change was queued: a same-scene world swap (`_pendingWorld`, from `QueueReplaceWorldOnCurrentScene`) takes priority; otherwise a full scene transition (`_pendingWorldTransition`, from `QueueWorldTransition`) is applied — optionally resetting the save, stopping SFX, notifying `IMurderGame.OnSceneTransition`, unpausing, switching the `SceneLoader` to the new world, and awaiting `LoadSceneAsync`. Called once per frame from `UpdateImpl`, before regular game logic runs.

#### UpdateImpl(Double)

```csharp
protected void UpdateImpl(double deltaTime)
```

Implements the core per-frame update logic given a raw delta time in seconds: applies pending exit/world-transition requests, handles frame-freeze (`FreezeFrames`), advances the unscaled and scaled (`TimeScale`/`IsPaused`-aware) clocks, updates `_playerInput`, runs as many fixed updates (`ActiveScene.FixedUpdate()`) as the accumulator allows (capped at 5 per frame, dropping the remainder and setting `LoosingFrames` if the cap is hit), calls `IMurderGame.OnUpdate()`, and finally runs `ActiveScene.Update()`. Note this takes a raw `double` number of seconds rather than a `GameTime`.

**Parameters** \
`deltaTime` [double](https://learn.microsoft.com/en-us/dotnet/api/System.Double?view=net-7.0) \

#### CanResumeAfterSaveComplete()

```csharp
public bool CanResumeAfterSaveComplete()
```

Determines if the game can resume after a save operation is complete. Returns `true` if there's no active save data or the save operation has finished (`GameDataManager.WaitPendingSaveTrackerOperation`).

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### QueueReplaceWorldOnCurrentScene(MonoWorld, Boolean)

```csharp
public bool QueueReplaceWorldOnCurrentScene(MonoWorld world, bool disposeWorld)
```

This is called when replacing the world for a current scene. Happens when transitioning between two different scenes (already loaded) sharing a world, rather than reloading a `WorldAsset` from scratch. Applied by `DoPendingWorldTransition` at the start of the next update.

**Parameters** \
`world` [MonoWorld](../Murder/Core/MonoWorld.html) \
`disposeWorld` [bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### QueueWorldTransition(Guid)

```csharp
public bool QueueWorldTransition(Guid world)
```

Schedules a transition to the world asset identified by `world` (a `WorldAsset` GUID). The actual swap happens at the start of the next frame so the current update completes cleanly. Returns `false` without effect if another transition is already queued.

**Parameters** \
`world` [Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### QueueWorldTransition(Guid, Boolean)

```csharp
public bool QueueWorldTransition(Guid world, bool resetSave)
```

Overload of `QueueWorldTransition(Guid)` that additionally marks the active save data to be reset once the transition is applied. Use this when transitioning to a new game/save slot rather than moving between levels of the same playthrough.

**Parameters** \
`world` [Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \
`resetSave` [bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### ResumeDeltaTimeOnUpdate()

```csharp
public bool ResumeDeltaTimeOnUpdate()
```

Resume game to normal game time, ending a `SkipDeltaTimeOnUpdate()` cutscene-skip. Returns whether the game was actually skipping beforehand.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### CreateRenderContext(GraphicsDevice, Camera2D, RenderContextFlags)

```csharp
public RenderContext CreateRenderContext(GraphicsDevice graphicsDevice, Camera2D camera, RenderContextFlags settings)
```

Creates a `RenderContext` using the specified graphics device, camera, and settings, delegating to `IMurderGame.CreateRenderContext` if present and otherwise constructing a default `RenderContext`. Implement `IMurderGame.CreateRenderContext` if your game needs a custom `RenderContext` subclass.

**Parameters** \
`graphicsDevice` [GraphicsDevice](https://docs.monogame.net/api/Microsoft.Xna.Framework.Graphics.GraphicsDevice.html) \
`camera` [Camera2D](../Murder/Core/Graphics/Camera2D.html) \
`settings` [RenderContextFlags](../Murder/Core/Graphics/RenderContextFlags.html) \

**Returns** \
[RenderContext](../Murder/Core/Graphics/RenderContext.html) \

#### GetDisplaySize()

```csharp
public Point GetDisplaySize()
```

Gets the size, in pixels, of the display the game window currently occupies (used for fullscreen mode). Combines SDL's display-bounds query with a DPI-scale correction derived by comparing pixel and logical window sizes.

**Returns** \
[Point](../Murder/Core/Geometry/Point.html) \

#### GetWindowSize()

```csharp
public Point GetWindowSize()
```

Gets the current size of the game window, in pixels, using SDL's window-size query (which accounts for OS-level DPI scaling). Falls back to `Window.ClientBounds` if SDL reports an invalid size. Prefer this over `DefaultWidth`/`DefaultHeight` when you need the actual, current window size.

**Returns** \
[Point](../Murder/Core/Geometry/Point.html) \

#### BeginImGuiTheme()

```csharp
public virtual void BeginImGuiTheme()
```

Placeholder called before each ImGui draw pass. Empty in the base `Game`; override in an editor subclass (e.g. `Architect`) to push custom style colors and variables onto the ImGui style stack.

#### Dispose()

```csharp
public virtual void Dispose()
```

Standard `IDisposable.Dispose()` implementation, inherited from `Microsoft.Xna.Framework.Game`. Calls `Dispose(true)` and suppresses finalization; the actual cleanup logic lives in `Dispose(bool)`.

#### EndImGuiTheme()

```csharp
public virtual void EndImGuiTheme()
```

Called after each ImGui draw pass. Empty in the base `Game`; override alongside `BeginImGuiTheme()` to pop any custom style colors and variables from the ImGui style stack.

#### OnUnhandledException(Exception)

```csharp
public virtual void OnUnhandledException(Exception ex)
```

Handles an exception that escaped normal game-loop error handling. Runs the shutdown steps normally performed on exit (`OnCloseImpl()`), captures a crash report via `GameLogger.CaptureCrash()`, and forwards the exception to `IMurderGame.OnFatalException(Exception)` as a last-resort hook before the process dies.

**Parameters** \
`ex` [Exception](https://learn.microsoft.com/en-us/dotnet/api/System.Exception?view=net-7.0) \

#### Exit()

```csharp
public void Exit()
```

Immediately signals MonoGame to stop the game loop and exit the process. Prefer `QueueExitGame()` over calling this directly to avoid disposing the world while it is actively being updated.

#### FreezeFrames(Int32)

```csharp
public void FreezeFrames(int amount)
```

This will pause the game for `amount` of frames. Implemented as a fixed-update-sized time budget consumed in `UpdateImpl` before regular simulation resumes; useful for hit-stop/screen-shake style effects.

**Parameters** \
`amount` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### OnWindowChange(WindowChangeNotification)

```csharp
public void OnWindowChange(WindowChangeNotification notification)
```

Queues a change to the game window (resolution, fullscreen toggle, or a plain resize notification). The change is not applied immediately; it is picked up and executed by `FlushWindow` the next time `Initialize` runs or a frame is drawn. Call this instead of touching `GraphicsDeviceManager` directly so the active scene is notified via `Scene.OnClientWindowChanged`.

**Parameters** \
`notification` [WindowChangeNotification](../Murder/Core/WindowChangeNotification.html) \

#### Pause()

```csharp
public void Pause()
```

This will pause the game.

#### QueueExitGame()

```csharp
public void QueueExitGame()
```

This queues such that the game exits at the end of the update. We wait until the end of the update to avoid any access to a world that has been disposed on cleanup.

#### ResetElapsedTime()

```csharp
public void ResetElapsedTime()
```

Resets the elapsed-time accumulator so the next frame receives a delta of zero. Useful after long loading pauses or debugging breaks to prevent a huge first-frame spike. Inherited from `Microsoft.Xna.Framework.Game`.

#### Resume()

```csharp
public void Resume()
```

This will resume the game.

#### Run()

```csharp
public void Run()
```

Starts the MonoGame event loop. Calls `Initialize`, `LoadContent`, then continuously calls `Update` and `Draw` until `Exit` is called. This is a blocking call — it returns only when the game closes. Inherited from `Microsoft.Xna.Framework.Game`.

#### RunOneFrame()

```csharp
public void RunOneFrame()
```

Advances the game by a single `Update`+`Draw` cycle. Used for unit tests or deterministic replay scenarios where the caller drives the game loop manually. Inherited from `Microsoft.Xna.Framework.Game`.

#### SetWaitForSaveComplete()

```csharp
public void SetWaitForSaveComplete()
```

Sets the flag to indicate that the game should wait for the in-flight save operation to complete before resuming normal updates (see `CanResumeAfterSaveComplete()`).

#### SkipDeltaTimeOnUpdate()

```csharp
public void SkipDeltaTimeOnUpdate()
```

This will skip update times and immediately run the update calls from the game until [Game.ResumeDeltaTimeOnUpdate](../Murder/Game.html#resumedeltatimeonupdate) is called. Used to fast-forward through cutscenes; also resets `StartedSkippingCutscene` to `false`.

#### SuppressDraw()

```csharp
public void SuppressDraw()
```

Tells MonoGame to skip the `Draw` call for the current frame. Use when the scene state hasn't changed and redrawing would be wasteful. Inherited from `Microsoft.Xna.Framework.Game`.

#### Tick()

```csharp
public void Tick()
```

Manually ticks one frame of the game loop (equivalent to a single `Update`+`Draw` step). Intended for headless testing or tooling scenarios where you control the loop. Inherited from `Microsoft.Xna.Framework.Game`.

⚡
