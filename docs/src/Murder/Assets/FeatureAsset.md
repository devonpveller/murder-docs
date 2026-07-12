# FeatureAsset

**Namespace:** Murder.Assets \
**Assembly:** Murder.dll

```csharp
public class FeatureAsset : GameAsset
```

A reusable, named bundle of ECS systems (and references to other `FeatureAsset`s) that can be toggled on or off as a unit and composed into a `WorldAsset`.

**Intent:** Let a project group related systems (e.g. "Combat", "Dialogue") into a single editor-authored asset instead of hand-picking individual systems in every world, and let nested features be enabled/disabled hierarchically.

**Use-case:** Create a `FeatureAsset` named "CombatFeature" and populate it with combat-related systems via the editor's feature UI (which calls `SetSystems`/`SetFeatures`). Reference it from a `WorldAsset` to enable those systems in that world; the world calls `FetchAllSystems` to flatten this feature (and any nested features it references) into the final system list. Set `IsDiagnostics` to automatically include it only in editor/diagnostic runs.

**Implements:** _[GameAsset](../../Murder/Assets/GameAsset.html)_

### ⭐ Constructors

```csharp
public FeatureAsset()
```

### ⭐ Properties

#### CanBeCreated

```csharp
public virtual bool CanBeCreated { get; }
```

Determines if the asset can be created, override to change this capability. Uses the inherited default (`true`).

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### CanBeDeleted

```csharp
public virtual bool CanBeDeleted { get; }
```

Determines if the asset can be deleted, override to change this capability. Uses the inherited default (`true`).

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### CanBeRenamed

```csharp
public virtual bool CanBeRenamed { get; }
```

Determines if the asset can be renamed, override to change this capability. Uses the inherited default (`true`).

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### CanBeSaved

```csharp
public virtual bool CanBeSaved { get; }
```

Determines if the asset can be saved, override to change this capability. Uses the inherited default (`true`).

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### EditorColor

```csharp
public override Vector4 EditorColor { get; }
```

Teal color (`#34ebcf`) used to visually distinguish `FeatureAsset` entries in the editor.

**Returns** \
[Vector4](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector4?view=net-7.0) \

#### EditorFolder

```csharp
public override string EditorFolder { get; }
```

Groups every `FeatureAsset` under a "Features" folder in the editor's asset tree.

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### FeaturesOnly

```csharp
public ImmutableArray<T> FeaturesOnly { get; }
```

The nested `FeatureAsset` references contained in this feature, each paired with whether that nested feature is currently active (each element is a `(Guid feature, bool isActive)` tuple). Use `FetchAllSystems` to flatten this hierarchy (together with `SystemsOnly`) into the final list of systems for a world.

**Returns** \
[ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \

#### FileChanged

```csharp
public bool FileChanged { get; public set; }
```

Whether this asset has unsaved modifications.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### FilePath

```csharp
public string FilePath { get; public set; }
```

Path to this asset file, relative to its base directory.

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### Guid

```csharp
public Guid Guid { get; protected set; }
```

Unique identifier for this feature, used to reference it from a `WorldAsset`'s system list or from another `FeatureAsset`'s `FeaturesOnly` list.

**Returns** \
[Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \

#### HasSystems

```csharp
public bool HasSystems { get; }
```

True if this feature (or, recursively, any of its active nested features) contains at least one system. Used by the editor/world building code to skip features that would contribute nothing.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### Icon

```csharp
public virtual char Icon { get; }
```

FontAwesome character icon displayed next to this asset in the editor.

**Returns** \
[char](https://learn.microsoft.com/en-us/dotnet/api/System.Char?view=net-7.0) \

#### IsDiagnostics

```csharp
public bool IsDiagnostics;
```

Whether this should always be added when running with diagnostics (e.g. editor). This will NOT be serialized into the world.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### IsStoredInSaveData

```csharp
public virtual bool IsStoredInSaveData { get; }
```

Whether this file is stored relative to the save path. Uses the inherited default (`false`).

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### Name

```csharp
public string Name { get; public set; }
```

Display name of this asset as shown in the editor.

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### Rename

```csharp
public bool Rename { get; public set; }
```

Whether the file should be renamed and the previous name deleted on next save.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### SaveLocation

```csharp
public virtual string SaveLocation { get; }
```

The folder path where this asset is saved on disk. Uses the inherited default.

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### StoreInDatabase

```csharp
public virtual bool StoreInDatabase { get; }
```

Whether this asset is stored following the database hierarchy. Uses the inherited default (`true`).

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### SystemsOnly

```csharp
public ImmutableArray<T> SystemsOnly { get; }
```

The raw ECS system type entries directly contained in this feature (excludes systems that come from nested `FeaturesOnly` references). Each entry is a `(Type systemType, bool isActive)` tuple pairing the system type with whether it is currently active.

**Returns** \
[ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \

#### TaggedForDeletion

```csharp
public bool TaggedForDeletion;
```

Marks this asset for removal on the next save.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

### ⭐ Methods

#### OnModified()

```csharp
protected virtual void OnModified()
```

Called by the editor when the asset is modified. `FeatureAsset` uses the inherited no-op default (it has no derived caches to clear).

#### Duplicate(string)

```csharp
public GameAsset Duplicate(string name)
```

Creates a deep copy of this asset with the given new name.

**Parameters** \
`name` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

**Returns** \
[GameAsset](../../Murder/Assets/GameAsset.html) \

#### FetchAllSystems(bool)

```csharp
public ImmutableArray<T> FetchAllSystems(bool enabled)
```

Recursively flattens this feature's own systems and every nested feature's systems into a single ordered list of `(Type systemType, bool isActive)` tuples. A system/nested feature is only active in the result if it is marked active AND `enabled` is true, so disabling a parent feature also disables everything nested inside it. `WorldAsset` calls this to build the final system list for a world.

**Parameters** \
`enabled` [bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

**Returns** \
[ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \

#### AssetsToBeSaved()

```csharp
public List<T> AssetsToBeSaved()
```

Returns and clears the list of dependent assets queued to be saved alongside this asset.

**Returns** \
[List\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Generic.List-1?view=net-7.0) \

#### GetSimplifiedName()

```csharp
public string GetSimplifiedName()
```

Returns the asset name stripped of any editor-folder prefix characters.

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### GetSplitNameWithEditorPath()

```csharp
public String[] GetSplitNameWithEditorPath()
```

Returns the display name split into path segments following the EditorFolder hierarchy.

**Returns** \
[string[]](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### AfterDeserialized()

```csharp
public virtual void AfterDeserialized()
```

Called after deserialization. `FeatureAsset` uses the inherited no-op default.

#### MakeGuid()

```csharp
public void MakeGuid()
```

Generates and assigns a new GUID to this asset.

#### SetFeatures(IList<T>)

```csharp
public void SetFeatures(IList<T> newSystemsList)
```

Replaces this feature's list of nested `FeatureAsset` references with `newSystemsList` (a list of `(Guid feature, bool isActive)` tuples). Used by the editor's feature editor when the user adds, removes, or toggles nested features.

**Parameters** \
`newSystemsList` [IList\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Generic.IList-1?view=net-7.0) \

#### SetSystems(IList<T>)

```csharp
public void SetSystems(IList<T> newList)
```

Replaces this feature's own list of ECS systems with `newList` (a list of `(Type systemType, bool isActive)` tuples). Used by the editor's feature editor when the user adds, removes, or reorders systems.

**Parameters** \
`newList` [IList\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Generic.IList-1?view=net-7.0) \

#### TrackAssetOnSave(Guid)

```csharp
public void TrackAssetOnSave(Guid g)
```

Queues a dependent asset by GUID to be saved whenever this asset is saved.

**Parameters** \
`g` [Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \

⚡
