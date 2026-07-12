# IMurderGame

**Namespace:** Murder \
**Assembly:** Murder.dll

```csharp
public abstract IMurderGame
```

This is the main loop of a murder game. This has the callbacks to relevant events in the game.

**Intent:** `IMurderGame` is the contract every Murder-based game implements to plug its game-specific logic into the engine. `Murder.Game` (the MonoGame `Game` subclass that owns the actual game loop) holds a reference to one `IMurderGame` instance and calls its lifecycle hooks (`Initialize`, `LoadContentAsync`, `OnUpdate`, `AfterDraw`, `OnSceneTransition`, `OnClose`, ...) at the appropriate points, and calls its factory methods (`CreateSoundPlayer`, `CreateRenderContext`, `CreateGameProfile`, `CreateSaveData`, ...) to obtain the concrete subsystem instances it should use. Every member has a default implementation, so a minimal game only needs to implement `Name`, `Options`, `ComponentsLookup`, and `GetDefaultFont()` (the members without a default body) and override whatever else it needs.

**Use-case:** Create a class implementing `IMurderGame`, pass an instance of it to the [Game](../Murder/Game.html) constructor, and call `Run()`. Override the lifecycle callbacks you need for game-specific behavior (e.g. `OnUpdate` for global input handling, `OnClose` to flush save data). Override the `Create*` factory methods to substitute custom subsystem implementations, such as a custom `ISoundPlayer` or `GameProfile` subclass. The Murder editor's `Architect` uses a specialization of this interface, [IMurderArchitect](../Murder.Editor/IMurderArchitect.html), which adds editor-only callbacks.

### ⭐ Properties

#### CanSave

```csharp
public virtual bool CanSave { get; }
```

Whether the game supports saving. Defaults to `true`. `Murder.Game.CanSave` reads this to decide whether save-related UI and logic should be exposed; return `false` for games that don't have persistent save data (e.g. some prototypes or arcade-style games).

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### ComponentsLookup

```csharp
public abstract virtual ComponentsLookup ComponentsLookup { get; }
```

Cache mapping every `IComponent` type used by the game to a stable index, generated automatically (via the Bang/Murder source generators) from the components declared in the game's assembly. `Murder.Game.Initialize` passes this to `World.InitializeLookupComponents` so entities can serialize/deserialize components by index. A game with no custom components can return `new MurderComponentsLookup()`.

**Returns** \
[ComponentsLookup](../Bang/ComponentsLookup.html) \

#### FeedbackUrl

```csharp
public virtual string FeedbackUrl { get; }
```

URL to report bugs or feedback, exposed statically via `Murder.Game.FeedbackUrl`. Defaults to an empty string. Override to point at your game's bug tracker or feedback form; the editor and crash-report tooling can surface this to testers.

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### GameHeight

```csharp
public virtual int GameHeight { get; }
```

Game's desired design-time display height, in pixels. Defaults to `180`. Read by `Murder.Game.DefaultHeight` and used, together with `GameWidth` and `Scale`, to compute the initial window size. Use [RenderContext.Camera](../Murder/Core/Graphics/RenderContext.html#camera) size for the actual runtime value.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### GameWidth

```csharp
public virtual int GameWidth { get; }
```

Game's desired design-time display width, in pixels. Defaults to `320`. Read by `Murder.Game.DefaultWidth` and used, together with `GameHeight` and `Scale`, to compute the initial window size. Use [RenderContext.Camera](../Murder/Core/Graphics/RenderContext.html#camera) size for the actual runtime value.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### HasCursor

```csharp
public virtual bool HasCursor { get; }
```

Whether the game renders and updates a visible mouse cursor. Combined with `Murder.Game.HasCursor` (either being `true` shows the cursor) to set `IsMouseVisible` when `Game` is constructed. Defaults to `true`; override to `false` for controller-only games.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### Name

```csharp
public abstract virtual string Name { get; }
```

This is the name of the game, used when creating assets. This is a required member with no default implementation — every game must supply one, typically the display/project name.

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### Options

```csharp
public abstract virtual JsonSerializerOptions Options { get; }
```

Serialization options used throughout the engine (asset saving/loading, save data) to (de)serialize game-specific types such as custom components and assets. This is generated automatically by the game's source-generated `JsonSerializerContext` based on the assets and components declared in its assembly; there is no default implementation.

**Returns** \
[JsonSerializerOptions](https://learn.microsoft.com/en-us/dotnet/api/System.Text.Json.JsonSerializerOptions?view=net-7.0) \

#### SaveName

```csharp
public virtual string SaveName { get; }
```

Name used specifically when loading/locating save data on disk. Defaults to `Name`. Override this if you want the save folder name to differ from the display name used for asset creation (for example, keeping saves compatible across a game rename).

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### Scale

```csharp
public virtual float Scale { get; }
```

Game's design-time pixel scaling factor. Defaults to `2`. Read by `Murder.Game.DefaultScale` and used together with `GameWidth`/`GameHeight` to compute the initial window size in pixels.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### Version

```csharp
public virtual float Version { get; }
```

This is the version of the game, used when checking for save compatibility. Defaults to `0`. `CreateSaveData(int)`'s default implementation stamps new save files with this value; bump it when you make a save-breaking change so `SaveData` loading logic can detect and handle older saves.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

### ⭐ Methods

#### AfterDraw()

```csharp
public virtual void AfterDraw()
```

Called once per frame after `Murder.Game` finishes drawing the active scene and its ImGui pass. Use this for any custom rendering that must happen after everything else, such as compositing an overlay directly onto the back buffer.

#### CreateGamePreferences()

```csharp
public virtual GamePreferences CreateGamePreferences()
```

Creates a custom game preferences instance for the game. Override to return a subclass of `GamePreferences` if your game needs extra persisted settings (e.g. custom graphics or accessibility options) beyond the engine defaults.

**Returns** \
[GamePreferences](../Murder/Save/GamePreferences.html) \

#### CreateGameProfile()

```csharp
public virtual GameProfile CreateGameProfile()
```

Creates a custom game profile for the game. Override to return a subclass of `GameProfile` if your game needs extra project-level configuration beyond the engine defaults (starting scene, grid size, target FPS, etc.).

**Returns** \
[GameProfile](../Murder/Assets/GameProfile.html) \

#### CreateRenderContext(GraphicsDevice, Camera2D, RenderContextFlags)

```csharp
public virtual RenderContext CreateRenderContext(GraphicsDevice graphicsDevice, Camera2D camera, RenderContextFlags settings)
```

Creates a custom render context for the game. `Murder.Game.CreateRenderContext` delegates here first, falling back to a plain `RenderContext` if this returns nothing custom. Override this only if your game needs a `RenderContext` subclass, for example to add extra render targets for a custom post-processing pipeline.

**Parameters** \
`graphicsDevice` [GraphicsDevice](https://docs.monogame.net/api/Microsoft.Xna.Framework.Graphics.GraphicsDevice.html) \
`camera` [Camera2D](../Murder/Core/Graphics/Camera2D.html) \
`settings` [RenderContextFlags](../Murder/Core/Graphics/RenderContextFlags.html) \

**Returns** \
[RenderContext](../Murder/Core/Graphics/RenderContext.html) \

#### CreateSaveData(Int32)

```csharp
public virtual SaveData CreateSaveData(int slot)
```

Creates a new `SaveData` instance for the given save slot. Defaults to `new SaveData(slot, Version)`, stamping the save with the game's current `Version`. Override to return a `SaveData` subclass if your game persists custom save-scoped state.

**Parameters** \
`slot` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

**Returns** \
[SaveData](../Murder/Assets/SaveData.html) \

#### CreateSaveDataInfo(Single, String)

```csharp
public virtual SaveDataInfo CreateSaveDataInfo(float version, string name)
```

Creates the lightweight `SaveDataInfo` record used to list/describe a save slot (e.g. in a save/load menu) without loading the full `SaveData`. Override if your game wants to attach extra metadata (playtime, chapter, thumbnail, etc.) to each save entry.

**Parameters** \
`version` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`name` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

**Returns** \
[SaveDataInfo](../Murder/Assets/Save/SaveDataInfo.html) \

#### CreateSaveTracker()

```csharp
public virtual SaveDataTracker CreateSaveTracker()
```

Creates the `SaveDataTracker` used to track pending/in-flight save operations for the active `SaveData`. Override only if your game needs custom tracking behavior around save completion (see `Murder.Game.SetWaitForSaveComplete` and `CanResumeAfterSaveComplete`).

**Returns** \
[SaveDataTracker](../Murder/Assets/Save/SaveDataTracker.html) \

#### CreateSoundPlayer()

```csharp
public virtual ISoundPlayer CreateSoundPlayer()
```

Creates the sound subsystem for the game, stored on `Murder.Game.SoundPlayer` and exposed statically via `Game.Sound`. Defaults to the engine's built-in `SoundPlayer`. Override to plug in a different audio backend.

**Returns** \
[ISoundPlayer](../Murder/Core/Sounds/ISoundPlayer.html) \

#### CreateWorldProcessor()

```csharp
public virtual WorldProcessor CreateWorldProcessor()
```

Creates the `WorldProcessor` used when loading a `WorldAsset` into a runtime `MonoWorld`. Override to inject custom entity/instance post-processing when worlds are instantiated (for example, game-specific setup that should run for every loaded level).

**Returns** \
[WorldProcessor](../Murder/Data/WorldProcessor.html) \

#### GetDefaultFont()

```csharp
public abstract virtual int GetDefaultFont()
```

Gets the default localization font that should be used for validating characters (i.e. checking that a font has glyphs for every character used by the game's text). This is a required member with no default implementation — every game must supply a valid font index.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### GetLocalizedFont(Int32)

```csharp
public virtual int GetLocalizedFont(int index)
```

Allows the game to override which font index is used for a given font slot based on the current localization/language settings — useful when a language (e.g. Japanese or Korean) needs a different font than the default. Defaults to returning `index` unchanged.

**Parameters** \
`index` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### Initialize()

```csharp
public virtual void Initialize()
```

Called once, when the executable for the game starts and initializes. This runs after `Murder.Game` has finished its own `Initialize` (input bindings registered, component lookup wired up) but before any content has been loaded. Use it for one-time setup that does not depend on assets, such as registering custom input buttons/axes or configuring third-party SDKs.

#### LoadContentAsync()

```csharp
public virtual Task LoadContentAsync()
```

This loads all the content within the game. Called after [IMurderGame.Initialize](../Murder/IMurderGame.html#initialize), from `Murder.Game.LoadSceneAsync`, before the initial scene finishes loading. Override to `await` any game-specific asynchronous content loading (e.g. warming caches, precomputing data) that must complete before the first scene is shown.

**Returns** \
[Task](https://learn.microsoft.com/en-us/dotnet/api/System.Threading.Tasks.Task?view=net-7.0) \

#### OnAfterContentLoaded()

```csharp
public virtual void OnAfterContentLoaded()
```

Called after content finishes loading. This is called *synchronously*, on the main thread, so it is safe to touch graphics resources or other main-thread-only state here, unlike `LoadContentAsync`.

#### OnClose()

```csharp
public virtual void OnClose()
```

Called once the game is shutting down. This runs both on a normal exit (`Murder.Game.QueueExitGame`/`Exit`) and when the process is terminated externally, since the engine wires it to `AppDomain.ProcessExit`. Use this to flush preferences, save data, or analytics before the process disappears; do not rely on it always having time to run async work.

#### OnFatalException(Exception)

```csharp
public virtual void OnFatalException(Exception ex)
```

Last resort callback before a fatal, unhandled exception takes down the game, invoked from `Murder.Game.OnUnhandledException`. Use this to attempt to save crash context, flush logs, or show a fallback error dialog; by the time this runs the game is already tearing down.

**Parameters** \
`ex` [Exception](https://learn.microsoft.com/en-us/dotnet/api/System.Exception?view=net-7.0) \

#### OnSceneTransition()

```csharp
public virtual void OnSceneTransition()
```

Called right before the engine swaps the active world, both for a full scene transition (`Murder.Game.QueueWorldTransition`) and a same-scene world replacement (`Murder.Game.QueueReplaceWorldOnCurrentScene`). Use this to tear down or persist any game-specific state that is scoped to the outgoing world before it is disposed.

#### OnUpdate()

```csharp
public virtual void OnUpdate()
```

Called once per frame from `Murder.Game`'s internal update, after all fixed updates and the active scene's own update have run. Use this for game-wide logic that is not tied to any single ECS system, such as global input handling that must react regardless of which scene is active.

#### TryCreatePreload()

```csharp
public virtual IPreloadGame? TryCreatePreload()
```

Creates an optional preload screen shown while the game's initial content is still loading. Defaults to `null` (no preload screen). Return an `IPreloadGame` implementation if your game needs a custom loading animation or splash screen; `Murder.Game` drives its `Update`/`Draw` calls (via `Murder.Game.OnLoadingDraw`) until the real content and initial scene are ready.

**Returns** \
[IPreloadGame](../Murder/Core/IPreloadGame.html) \

⚡
