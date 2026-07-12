# AtlasId

**Namespace:** Murder.Data \
**Assembly:** Murder.dll

```csharp
public sealed enum AtlasId : Enum, IComparable, ISpanFormattable, IFormattable, IConvertible
```

**Implements:** _[Enum](https://learn.microsoft.com/en-us/dotnet/api/System.Enum?view=net-7.0), [IComparable](https://learn.microsoft.com/en-us/dotnet/api/System.IComparable?view=net-7.0), [ISpanFormattable](https://learn.microsoft.com/en-us/dotnet/api/System.ISpanFormattable?view=net-7.0), [IFormattable](https://learn.microsoft.com/en-us/dotnet/api/System.IFormattable?view=net-7.0), [IConvertible](https://learn.microsoft.com/en-us/dotnet/api/System.IConvertible?view=net-7.0)_

**Intent:** An editor/import-time label for which texture atlas an imported sprite should be packed into. Each importer (e.g. `AsepriteImporter_Gameplay`, `AsepriteImporter_Editor`, `AsepriteImporter_Preload`, `CutsceneAsepriteImporter`) exposes a fixed `AtlasId` that it hands to the packer for every asset it produces.

**Use-case:** `AtlasId` itself never reaches the runtime atlas-lookup APIs directly — [GameDataManager](../../Murder/Data/GameDataManager.html) methods such as `FetchAtlas`/`TryFetchAtlas`/`DisposeAtlas`/`ReplaceAtlas` take the plain `string` atlas name instead. The bridge between the two is the `[Description]` attribute on each enum value (read via the `GetDescription()` extension method), which maps the enum value to the actual atlas filename constant declared on `AtlasIdentifiers` (e.g. `AtlasId.Gameplay` → `AtlasIdentifiers.Gameplay` → `"atlas"`). Use `AtlasId` when writing or configuring an importer that needs to say "pack this asset's sprites into atlas X"; use `AtlasIdentifiers`'s string constants (or an asset's own `Atlas`/`AtlasId` string field) when calling into `GameDataManager` at runtime.

### ⭐ Properties

#### None

```csharp
public static const AtlasId None;
```

Default/unset value. An asset or importer left at `None` has not been assigned to any atlas; it has no `[Description]` and therefore no corresponding entry in `AtlasIdentifiers`.

**Returns** \
[AtlasId](../../Murder/Data/AtlasId.html) \

#### Gameplay

```csharp
public static const AtlasId Gameplay;
```

The main atlas used by `AsepriteImporter_Gameplay` for regular in-game sprites (characters, props, effects). Maps to `AtlasIdentifiers.Gameplay` (`"atlas"`) and is the atlas `GameDataManager.AfterContentLoadedFromMainThread` eagerly loads textures for after content finishes loading.

**Returns** \
[AtlasId](../../Murder/Data/AtlasId.html) \

#### Editor

```csharp
public static const AtlasId Editor;
```

Atlas for editor-only UI icons and sprites (used by `AsepriteImporter_Editor`), never required by a shipped release build. Maps to `AtlasIdentifiers.Editor` (`"editor"`); `TextureAtlas`'s built-in "missing image" placeholder is fetched from this atlas.

**Returns** \
[AtlasId](../../Murder/Data/AtlasId.html) \

#### Static

```csharp
public static const AtlasId Static;
```

Default atlas for imported PNGs (see `PngImporter`) that are not otherwise categorized. Maps to `AtlasIdentifiers.Static` (`"static"`).

**Returns** \
[AtlasId](../../Murder/Data/AtlasId.html) \

#### Temporary

```csharp
public static const AtlasId Temporary;
```

Fallback target atlas used by `AsepriteImporter` for assets that don't belong to one of the other named atlases. Maps to `AtlasIdentifiers.Temporary` (`"temporary"`).

**Returns** \
[AtlasId](../../Murder/Data/AtlasId.html) \

#### Preload

```csharp
public static const AtlasId Preload;
```

Atlas for sprites used by `AsepriteImporter_Preload`, packed alongside `PreloadPackedGameData` so they are available during the earliest loading-screen phase, before the rest of the game's content has loaded. Maps to `AtlasIdentifiers.Preload` (`"preload"`).

**Returns** \
[AtlasId](../../Murder/Data/AtlasId.html) \

#### Cutscenes

```csharp
public static const AtlasId Cutscenes;
```

Atlas dedicated to cutscene sprites, populated by `AsepriteImporter_Cutscene`/`CutsceneAsepriteImporter`. Maps to `AtlasIdentifiers.Cutscenes` (`"cutscenes"`).

**Returns** \
[AtlasId](../../Murder/Data/AtlasId.html) \

⚡
