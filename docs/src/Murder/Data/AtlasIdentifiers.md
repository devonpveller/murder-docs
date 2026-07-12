# AtlasIdentifiers

**Namespace:** Murder.Data \
**Assembly:** Murder.dll

```csharp
public static class AtlasIdentifiers
```

Holds the actual atlas filename (without extension) for each built-in atlas, as a plain `string` constant.

**Intent:** [GameDataManager](../../Murder/Data/GameDataManager.html)'s atlas APIs (`FetchAtlas`, `TryFetchAtlas`, `ReplaceAtlas`, `DisposeAtlas`) key loaded atlases by `string` name rather than by the [AtlasId](../../Murder/Data/AtlasId.html) enum, since atlas filenames are also referenced from serialized data (e.g. a `SpriteAsset`'s `Atlas` field, or `ReferencedAtlas.Id`) that has no dependency on the editor-only `AtlasId` enum. `AtlasIdentifiers` is the single place these string literals are declared, and each `AtlasId` enum value's `[Description]` attribute points back to one of these constants so the two stay in sync.

**Use-case:** Pass one of these constants directly to `GameDataManager.FetchAtlas`/`TryFetchAtlas` when you need a specific built-in atlas at runtime (e.g. `Game.Data.TryFetchAtlas(AtlasIdentifiers.Editor)` to draw an editor icon, or `Game.Data.FetchAtlas(AtlasIdentifiers.Gameplay)` to preload the main gameplay atlas), instead of hardcoding the raw string.

### ⭐ Properties

#### Gameplay

```csharp
public static const string Gameplay;
```

Filename (`"atlas"`) of the main gameplay sprite atlas.

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### Editor

```csharp
public static const string Editor;
```

Filename (`"editor"`) of the editor-only icon/UI atlas.

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### Static

```csharp
public static const string Static;
```

Filename (`"static"`) of the atlas used for imported PNGs that don't belong to a more specific atlas.

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### Temporary

```csharp
public static const string Temporary;
```

Filename (`"temporary"`) of the fallback atlas used for assets imported without an explicit atlas assignment.

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### Preload

```csharp
public static const string Preload;
```

Filename (`"preload"`) of the atlas packed alongside `PreloadPackedGameData` and loaded during the earliest loading-screen phase.

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### Cutscenes

```csharp
public static const string Cutscenes;
```

Filename (`"cutscenes"`) of the atlas dedicated to cutscene sprites.

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

⚡
