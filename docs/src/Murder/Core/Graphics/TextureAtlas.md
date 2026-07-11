# TextureAtlas

**Namespace:** Murder.Core.Graphics \
**Assembly:** Murder.dll

```csharp
public class TextureAtlas : IDisposable
```

A texture atlas, the texture2D can be loaded and unloaded from the GPU at any time
            We will keep the texture lists in memory all the time, though.

**Intent:** Provides a named sprite sheet that maps string identifiers to `AtlasCoordinates`, allowing efficient batched rendering from a shared GPU texture.

**Use-case:** Retrieve via `Game.Data.FetchAtlas()` and call `Get()` to look up `AtlasCoordinates` for sprite draw calls, or `TryGet()` when the sprite may not exist.

**Implements:** _[IDisposable](https://learn.microsoft.com/en-us/dotnet/api/System.IDisposable?view=net-7.0)_

### ⭐ Constructors
```csharp
public TextureAtlas(string name, AtlasId id)
```

**Parameters** \
`name` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
`id` [AtlasId](../../../Murder/Data/AtlasId.html) \

### ⭐ Properties
#### CountEntries
```csharp
public int CountEntries { get; }
```

Total number of named sprite entries registered in this atlas.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
#### Id
```csharp
public readonly AtlasId Id;
```

The `AtlasId` enum value identifying which packed atlas this instance corresponds to.

**Returns** \
[AtlasId](../../../Murder/Data/AtlasId.html) \
#### Name
```csharp
public readonly string Name;
```

String identifier used when loading and referencing this atlas on disk.

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
### ⭐ Methods
#### Get(string)
```csharp
public AtlasCoordinates Get(string id)
```

Returns the `AtlasCoordinates` for the sprite with the given identifier, or falls back to the `missingImage` placeholder if not found.

**Parameters** \
`id` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

**Returns** \
[AtlasCoordinates](../../../Murder/Core/Graphics/AtlasCoordinates.html) \

#### HasId(string)
```csharp
public bool HasId(string id)
```

Returns true if a sprite is registered under the given identifier in this atlas.

**Parameters** \
`id` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### TryCreateTexture(string, out Texture2D&)
```csharp
public bool TryCreateTexture(string id, Texture2D& texture)
```

Attempts to extract the named sprite as a standalone `Texture2D` at 1:1 scale; returns false if the sprite is not found. The returned texture must be manually disposed.

**Parameters** \
`id` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
`texture` [Texture2D&](https://docs.monogame.net/api/Microsoft.Xna.Framework.Graphics.Texture2D.html) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### TryGet(string, out AtlasCoordinates&)
```csharp
public bool TryGet(string id, AtlasCoordinates& coord)
```

Attempts to retrieve the atlas coordinates for the given identifier without falling back to a placeholder; returns false if not found.

**Parameters** \
`id` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
`coord` [AtlasCoordinates&](../../../Murder/Core/Graphics/AtlasCoordinates.html) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### GetAllEntries()
```csharp
public IEnumerable<T> GetAllEntries()
```

Returns all registered `AtlasCoordinates` entries in this atlas.

**Returns** \
[IEnumerable\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Generic.IEnumerable-1?view=net-7.0) \

#### CreateTextureFromAtlas(AtlasCoordinates, SurfaceFormat, float)
```csharp
public Texture2D CreateTextureFromAtlas(AtlasCoordinates textureCoord, SurfaceFormat format, float scale)
```

This creates a new texture on the fly and should be *AVOIDED!*. Use `Get` instead.

**Parameters** \
`textureCoord` [AtlasCoordinates](../../../Murder/Core/Graphics/AtlasCoordinates.html) \
\
`format` [SurfaceFormat](https://docs.monogame.net/api/Microsoft.Xna.Framework.Graphics.SurfaceFormat.html) \
\
`scale` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
\

**Returns** \
[Texture2D](https://docs.monogame.net/api/Microsoft.Xna.Framework.Graphics.Texture2D.html) \

#### CreateTextureFromAtlas(string)
```csharp
public Texture2D CreateTextureFromAtlas(string id)
```

This creates a new texture on the fly and should be *AVOIDED!*. Use `Get` instead.

**Parameters** \
`id` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

**Returns** \
[Texture2D](https://docs.monogame.net/api/Microsoft.Xna.Framework.Graphics.Texture2D.html) \

#### Dispose()
```csharp
public virtual void Dispose()
```

Releases all GPU textures held by this atlas.

#### LoadTextures()
```csharp
public void LoadTextures()
```

Loads the packed atlas texture files from disk into GPU memory; called automatically on first access if textures have not been loaded.

#### PopulateAtlas(IEnumerable<T>)
```csharp
public void PopulateAtlas(IEnumerable<T> entries)
```

Registers a collection of named sprite coordinates into the atlas lookup table, replacing any previous contents.

**Parameters** \
`entries` [IEnumerable\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Generic.IEnumerable-1?view=net-7.0) \

#### UnloadTextures()
```csharp
public void UnloadTextures()
```

Unloads GPU textures from memory while retaining the coordinate lookup table, allowing textures to be reloaded later.

⚡