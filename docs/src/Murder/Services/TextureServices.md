# TextureServices

**Namespace:** Murder.Services \
**Assembly:** Murder.dll

```csharp
public static class TextureServices
```

Utilities for loading `Texture2D` assets from disk, supporting both PNG and QOI+GZ formats.

**Intent:** Abstracts format-aware texture loading so game code can load images without knowing the underlying file format.

**Use-case:** Call `FromFile` to load any supported texture from a file path during asset loading or hot-reload operations.

### ⭐ Properties
#### PNG_EXTENSION
```csharp
public static const string PNG_EXTENSION;
```
File extension constant for PNG images (`.png`).

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
#### QOI_GZ_EXTENSION
```csharp
public static const string QOI_GZ_EXTENSION;
```
File extension constant for gzip-compressed QOI images (`.qoi.gz`), the engine's preferred packed texture format.

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
### ⭐ Methods
#### FromFile(GraphicsDevice, string)
```csharp
public Texture2D FromFile(GraphicsDevice graphicsDevice, string path)
```
Loads a `Texture2D` from `path`, automatically detecting whether the file is PNG or QOI+GZ format.

**Parameters** \
`graphicsDevice` [GraphicsDevice](https://docs.monogame.net/api/Microsoft.Xna.Framework.Graphics.GraphicsDevice.html) \
`path` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

**Returns** \
[Texture2D](https://docs.monogame.net/api/Microsoft.Xna.Framework.Graphics.Texture2D.html) \



⚡