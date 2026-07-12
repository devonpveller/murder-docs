# TextureServices

**Namespace:** Murder.Services \
**Assembly:** Murder.dll

```csharp
public static class TextureServices
```

Utility for loading a `Texture2D` from disk, transparently handling the engine's gzip-compressed QOI texture format alongside standard image formats.

**Intent:** Abstracts format-aware texture loading so asset-loading code can load a texture from a file path without knowing (or caring) whether it was packed as `.qoi.gz` or left as a plain image file.

**Use-case:** Call `FromFile` wherever a raw `Texture2D` needs to be loaded from disk during asset loading, hot-reload, or editor tooling — for example loading atlas pages or standalone textures that aren't routed through the `SpriteAsset` pipeline.

### ⭐ Properties

#### PNG_EXTENSION

```csharp
public const string PNG_EXTENSION = ".png";
```

File extension constant for PNG images.

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### QOI_GZ_EXTENSION

```csharp
public const string QOI_GZ_EXTENSION = ".qoi.gz";
```

File extension constant for gzip-compressed QOI images, the engine's preferred packed texture format. `FromFile` checks for this suffix to decide whether to decompress before decoding.

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

### ⭐ Methods

#### FromFile(GraphicsDevice, string)

```csharp
public static Texture2D FromFile(GraphicsDevice graphicsDevice, string path)
```

Loads a `Texture2D` from `path`. If the path ends with `.qoi.gz`, the file is first gzip-decompressed in memory and the resulting QOI data is decoded via `Texture2D.FromStream`; otherwise the file is passed to `Texture2D.FromStream` directly (supporting any format MonoGame/FNA can decode, e.g. PNG). If `path` does not exist, logs an error and returns a fallback 1x1 pixel texture instead of throwing.

**Parameters** \
`graphicsDevice` [GraphicsDevice](https://docs.monogame.net/api/Microsoft.Xna.Framework.Graphics.GraphicsDevice.html) \
`path` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

**Returns** \
[Texture2D](https://docs.monogame.net/api/Microsoft.Xna.Framework.Graphics.Texture2D.html) \

⚡
