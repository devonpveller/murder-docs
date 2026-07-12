# SpriteEventDataManagerAsset

**Namespace:** Murder.Editor.Assets \
**Assembly:** Murder.dll

```csharp
public class SpriteEventDataManagerAsset : GameAsset
```

Singleton, engine-created asset that stores every sprite's custom event overrides for the whole project, indexed by sprite GUID.

**Intent:** Serves as the single project-wide registry of per-sprite, per-animation event customizations made in the sprite/animation editor. There is only ever one instance per project; the editor's data manager finds or lazily creates it rather than letting the developer create one from the asset browser, which is why it is hidden from the UI (tucked under [GameDataManager.HiddenAssetsRelativePath](../../../Murder/Data/GameDataManager.html#hiddenassetsrelativepath), which itself starts with [GameDataManager.SKIP_CHAR](../../../Murder/Data/GameDataManager.html#skip_char)).

**Use-case:** Queried during atlas/sprite import (via `EditorDataManager.TryGetSpriteEventData`/`GetOrCreateSpriteEventData`) to merge custom [SpriteEventData](../../../Murder/Editor/Assets/SpriteEventData.html) overrides into generated sprite asset animations.

**Implements:** _[GameAsset](../../../Murder/Assets/GameAsset.html)_

### ⭐ Constructors

```csharp
public SpriteEventDataManagerAsset()
```

Creates a new, empty manager asset. Normally you should not call this directly -- use the editor's data manager to fetch the single project-wide instance instead of creating a competing one.

### ⭐ Properties

#### CanBeCreated

```csharp
public virtual bool CanBeCreated { get; }
```

Not overridden by this type; inherits `GameAsset`'s default of `true`. In practice the asset is never created from the browser because it is hidden via `HideInEditor`.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### CanBeDeleted

```csharp
public virtual bool CanBeDeleted { get; }
```

Not overridden by this type; inherits `GameAsset`'s default of `true`.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### CanBeRenamed

```csharp
public virtual bool CanBeRenamed { get; }
```

Not overridden by this type; inherits `GameAsset`'s default of `true`.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### CanBeSaved

```csharp
public virtual bool CanBeSaved { get; }
```

Not overridden by this type; inherits `GameAsset`'s default of `true`.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### EditorColor

```csharp
public virtual Vector4 EditorColor { get; }
```

Not overridden by this type; inherits `GameAsset`'s default, which ties the icon color to `Game.Profile.Theme.White`.

**Returns** \
[Vector4](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector4?view=net-7.0) \

#### EditorFolder

```csharp
public override string EditorFolder { get; }
```

Returns [GameDataManager.HiddenAssetsRelativePath](../../../Murder/Data/GameDataManager.html#hiddenassetsrelativepath) (`"_Hidden"`), which starts with [GameDataManager.SKIP_CHAR](../../../Murder/Data/GameDataManager.html#skip_char) so the editor's asset tree skips rendering this asset entirely.

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### Events

```csharp
public ImmutableDictionary<Guid, SpriteEventData> Events { get; }
```

Immutable map from sprite GUID to that sprite's custom event overrides. Read by the sprite importer at atlas-build time to merge manual event edits into the generated sprite asset's animations, and written to via [GetOrCreate(Guid)](../../../Murder/Editor/Assets/SpriteEventDataManagerAsset.html#getorcreateguid) whenever the developer edits events in the sprite editor.

**Returns** \
[ImmutableDictionary\<Guid, SpriteEventData\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableDictionary-2?view=net-7.0) \

#### FileChanged

```csharp
public bool FileChanged { get; set; }
```

Whether this asset has been modified since it was last saved to disk. Setting this to `true` also invokes `OnModified` so subclasses can clear derived caches.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### FilePath

```csharp
public string FilePath { get; set; }
```

Path to this asset file, relative to its base directory where this asset is stored.

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### Guid

```csharp
public Guid Guid { get; protected set; }
```

Globally unique identifier for this asset instance.

**Returns** \
[Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \

#### Icon

```csharp
public virtual char Icon { get; }
```

Not overridden by this type; inherits `GameAsset`'s default icon glyph. Irrelevant in practice since the asset is hidden from the browser.

**Returns** \
[char](https://learn.microsoft.com/en-us/dotnet/api/System.Char?view=net-7.0) \

#### IsStoredInSaveData

```csharp
public virtual bool IsStoredInSaveData { get; }
```

Not overridden by this type; inherits `GameAsset`'s default of `false`, so this asset is packed with regular game assets rather than stored alongside save data.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### Name

```csharp
public string Name { get; set; }
```

Display name of this asset.

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### Rename

```csharp
public bool Rename { get; set; }
```

Whether it should rename the file and delete the previous name.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### SaveLocation

```csharp
public virtual string SaveLocation { get; }
```

Not overridden by this type; inherits `GameAsset`'s default, deriving the save folder from `Game.Profile.GenericAssetsPath` combined with `EditorFolder`.

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### StoreInDatabase

```csharp
public virtual bool StoreInDatabase { get; }
```

Not overridden by this type; inherits `GameAsset`'s default of `true`.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### TaggedForDeletion

```csharp
public bool TaggedForDeletion;
```

Marks this asset for removal from disk the next time the asset database saves.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

### ⭐ Methods

#### OnModified()

```csharp
protected virtual void OnModified()
```

Not overridden by this type; inherits `GameAsset`'s no-op default.

#### DeleteSprite(Guid)

```csharp
public bool DeleteSprite(Guid spriteId)
```

Stops tracking custom event overrides for the sprite identified by `spriteId`, e.g. when that sprite asset is deleted from the project.

**Parameters** \
`spriteId` [Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) -- GUID of the sprite whose event overrides should be discarded. \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) -- `true` if the sprite had tracked event data that was removed; `false` if it had none. \

#### Duplicate(string)

```csharp
public GameAsset Duplicate(string name)
```

Create a deep copy of this asset with the given new name.

**Parameters** \
`name` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

**Returns** \
[GameAsset](../../../Murder/Assets/GameAsset.html) \

#### AssetsToBeSaved()

```csharp
public List<T> AssetsToBeSaved()
```

Return the assets which will be saved with this asset. Also clears the pending list.

**Returns** \
[List\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Generic.List-1?view=net-7.0) \

#### GetOrCreate(Guid)

```csharp
public SpriteEventData GetOrCreate(Guid spriteId)
```

Returns the [SpriteEventData](../../../Murder/Editor/Assets/SpriteEventData.html) overrides for `spriteId`, creating and registering an empty one if this sprite has never had any custom events before. Use this (rather than reading `Events` directly) whenever the caller intends to add or remove an override, since it guarantees a non-null instance to mutate.

**Parameters** \
`spriteId` [Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) -- GUID of the sprite to fetch or create override data for. \

**Returns** \
[SpriteEventData](../../../Murder/Editor/Assets/SpriteEventData.html) \

#### GetSimplifiedName()

```csharp
public string GetSimplifiedName()
```

Returns just the last segment of the asset's editor path -- i.e. `Name` with any leading editor-folder path stripped off.

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### GetSplitNameWithEditorPath()

```csharp
public String[] GetSplitNameWithEditorPath()
```

Returns `Name` combined with `EditorFolder` and split into path segments.

**Returns** \
[string[]](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### AfterDeserialized()

```csharp
public virtual void AfterDeserialized()
```

Not overridden by this type; inherits `GameAsset`'s no-op default.

#### MakeGuid()

```csharp
public void MakeGuid()
```

Generates and assigns a new globally unique identifier (GUID) to the object.

#### TrackAssetOnSave(Guid)

```csharp
public void TrackAssetOnSave(Guid g)
```

Track an asset such that `g` is also saved once this asset is saved.

**Parameters** \
`g` [Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \

⚡
