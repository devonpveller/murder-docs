# TextureAtlas

**Namespace:** Murder.Core.Graphics \
**Assembly:** Murder.dll

```csharp
public class TextureAtlas : IDisposable
```

A texture atlas: the underlying `Texture2D` pages can be loaded and unloaded from the GPU at any time, but the sprite coordinate lookup table is kept in memory at all times.

**Intent:** Maps string sprite identifiers to `AtlasCoordinates` within one or more packed GPU texture pages, so many individual images can be rendered from a small number of large shared textures. This is central to sprite batching: as long as sprites come from the same atlas texture, they can be drawn together without switching GPU textures between draw calls.

**Use-case:** Retrieve an existing atlas via `Game.Data.FetchAtlas()` (or `Assets.Get*` helpers) and call `Get()` to look up `AtlasCoordinates` for a sprite draw call, or `TryGet()` when the sprite may legitimately not exist. Constructing a `TextureAtlas` directly is normally only done by the asset packing/importing pipeline (e.g. `AsepriteImporter`), which then calls `PopulateAtlas()`/`AddEntry()` to fill it in.

**Implements:** _[IDisposable](https://learn.microsoft.com/en-us/dotnet/api/System.IDisposable?view=net-7.0)_

### ⭐ Constructors

```csharp
public TextureAtlas(string atlasId)
```

Creates an empty atlas with the given id. The atlas holds no sprite entries and no loaded textures until `PopulateAtlas()`/`AddEntry()` and `LoadTextures()` (or first access to `Textures`) are called; this is normally done by the asset packing/loading pipeline rather than directly by game code.

**Parameters** \
`atlasId` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

### ⭐ Properties

#### AtlasId

```csharp
public readonly string AtlasId;
```

Identifier of this atlas (e.g. "editor", "gameplay"), used both as the key it is registered under and as the on-disk file name prefix for its packed pages, e.g. "{AtlasId}000.qoi.gz", "{AtlasId}001.qoi.gz", etc.

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### CountEntries

```csharp
public int CountEntries { get; }
```

Total number of named sprite entries registered in this atlas.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### Textures

```csharp
public Texture2D[] Textures { get; }
```

The GPU texture pages backing this atlas, one per packed image file on disk. Accessing this property loads the textures from disk on first use (via `LoadTextures()`) if they have not been loaded yet, so the first access after a call to `UnloadTextures()` may be slow.

**Returns** \
[Texture2D[]](https://docs.monogame.net/api/Microsoft.Xna.Framework.Graphics.Texture2D.html) \

### ⭐ Methods

#### Get(string)

```csharp
public AtlasCoordinates Get(string id)
```

Returns the `AtlasCoordinates` registered under `id`. If the sprite is not found, logs it and falls back to the "missingImage" placeholder from the editor atlas, so this is the convenient default for sprite lookups that are expected to always resolve. Use `TryGet()` instead when a missing sprite is an expected, non-error condition.

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

#### TryCreateTexture(string, out Texture2D&, float)

```csharp
public bool TryCreateTexture(string id, Texture2D& texture, float scale)
```

Attempts to extract the named sprite as a standalone `Texture2D` at the given scale by drawing it into a fresh render target; returns false if the sprite is not found or extraction fails. The returned texture must be manually disposed.

**Parameters** \
`id` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
`texture` [Texture2D&](https://docs.monogame.net/api/Microsoft.Xna.Framework.Graphics.Texture2D.html) \
`scale` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### TryGet(string, out AtlasCoordinates&)

```csharp
public bool TryGet(string id, AtlasCoordinates& coord)
```

Attempts to retrieve the `AtlasCoordinates` registered under `id` without falling back to a placeholder image. Prefer this over `Get()` whenever the sprite might legitimately be missing (e.g. optional visuals), to avoid the log spam and placeholder lookup that `Get()` performs on a miss.

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
public Texture2D CreateTextureFromAtlas(AtlasCoordinates textureCoord, SurfaceFormat format = SurfaceFormat.Color, float scale = 1)
```

This creates a new texture on the fly and should be _AVOIDED!_. Use `Get` instead.

**Parameters** \
`textureCoord` [AtlasCoordinates](../../../Murder/Core/Graphics/AtlasCoordinates.html) \
`format` [SurfaceFormat](https://docs.monogame.net/api/Microsoft.Xna.Framework.Graphics.SurfaceFormat.html) \
`scale` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

**Returns** \
[Texture2D](https://docs.monogame.net/api/Microsoft.Xna.Framework.Graphics.Texture2D.html) \

#### CreateTextureFromAtlas(string, float)

```csharp
public Texture2D CreateTextureFromAtlas(string id, float scale)
```

This creates a new texture on the fly and should be _AVOIDED!_. Use `Get` instead.

**Parameters** \
`id` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
`scale` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

**Returns** \
[Texture2D](https://docs.monogame.net/api/Microsoft.Xna.Framework.Graphics.Texture2D.html) \

#### AddEntry(string, AtlasCoordinates)

```csharp
public void AddEntry(string id, AtlasCoordinates coord)
```

Registers or replaces a single sprite entry in this atlas's lookup table. Unlike `PopulateAtlas()`, this adds one entry incrementally without touching the rest of the table; used e.g. by the editor/import pipeline (`AsepriteImporter`) to patch in a single changed sprite.

**Parameters** \
`id` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
`coord` [AtlasCoordinates](../../../Murder/Core/Graphics/AtlasCoordinates.html) \

#### Dispose()

```csharp
public void Dispose()
```

Releases all GPU textures held by this atlas (via `UnloadTextures()`) and clears the sprite coordinate lookup table, leaving the atlas empty.

#### LoadTextures()

```csharp
public void LoadTextures()
```

Loads the packed atlas texture files from disk into GPU memory; called automatically on first access to `Textures` if they have not been loaded yet.

#### PopulateAtlas(IEnumerable<T>)

```csharp
public void PopulateAtlas(IEnumerable<T> entries)
```

Replaces the entire sprite lookup table with `entries`, keyed by escaped id. Used by the asset packing pipeline to (re)populate an atlas after packing a batch of images; existing entries not present in `entries` are dropped.

**Parameters** \
`entries` [IEnumerable\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Generic.IEnumerable-1?view=net-7.0) \

#### UnloadTextures()

```csharp
public void UnloadTextures()
```

Disposes and releases all currently loaded GPU texture pages, freeing GPU memory while keeping the sprite coordinate lookup table intact. The textures will be transparently reloaded from disk the next time `Textures` is accessed or `LoadTextures()` is called. Useful for freeing rarely-used atlases (e.g. editor-only or level-specific ones) without losing their metadata.

⚡
