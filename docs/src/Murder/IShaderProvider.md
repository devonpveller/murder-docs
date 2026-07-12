# IShaderProvider

**Namespace:** Murder \
**Assembly:** Murder.dll

```csharp
public abstract IShaderProvider
```

A game that leverages murder and use custom shaders should implement this in their [IMurderGame](../Murder/IMurderGame.html).

**Intent:** `IShaderProvider` is an optional interface a game's `IMurderGame` implementation can also implement to supply its own compiled shader effects to the renderer, on top of the engine's built-in `sprite2d`, `simple`, and `pixel_art_murder` shaders.

**Use-case:** When your game needs a custom post-processing effect, a special sprite shader, or any other non-default GPU effect, make your `IMurderGame` class also implement `IShaderProvider` and return the shader file names (no extension) from `Shaders`. `GameDataManager.LoadShaders` — called from `Game.LoadContent` and again on hot-reload — detects the interface via `_game is IShaderProvider provider` and loads each named `.fxb` file from the `resources` folder into a parallel `GameDataManager.CustomGameShaders` array (`CustomGameShaders[i]` corresponds to `Shaders[i]`), which your rendering code can then look up by index. If your `IMurderGame` implementation does not also implement `IShaderProvider`, no custom shaders are loaded.

### ⭐ Properties

#### Shaders

```csharp
public abstract virtual String[] Shaders { get; }
```

Names of custom compiled shader (`.fxb`) files this game provides, without extension. Each name is expected to be placed alongside the engine's built-in shaders at `<game_directory>/../resources`. The engine loads every entry in this array, in order, into `GameDataManager.CustomGameShaders` during `LoadShaders`, so index `i` in `Shaders` corresponds to index `i` in `CustomGameShaders`.

**Returns** \
[string[]](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

⚡
