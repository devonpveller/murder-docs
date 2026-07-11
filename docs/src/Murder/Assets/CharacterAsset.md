# CharacterAsset

**Namespace:** Murder.Assets \
**Assembly:** Murder.dll

```csharp
public class CharacterAsset : GameAsset
```

Defines a dialogue character asset containing all `Situation` dialogue trees and per-dialogue-line metadata for a single NPC.

**Intent:** Link a `SpeakerAsset` owner to a named set of dialogue trees and store per-line overrides such as custom portraits and ECS components triggered during conversation.

**Use-case:** Create one `CharacterAsset` per speaking character. Reference it from a `DialogueComponent` to run dialogue at runtime. Call `TryFetchSituation` to retrieve a branch by name, and use the editor's custom-portrait and custom-component fields to override visuals or trigger events on individual dialogue lines.

**Implements:** _[GameAsset](../../Murder/Assets/GameAsset.html)_

### ⭐ Constructors
```csharp
public CharacterAsset()
```

### ⭐ Properties
#### CanBeCreated
```csharp
public virtual bool CanBeCreated { get; }
```

Determines if the asset can be created, override to change this capability.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
#### CanBeDeleted
```csharp
public virtual bool CanBeDeleted { get; }
```

Determines if the asset can be deleted, override to change this capability.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
#### CanBeRenamed
```csharp
public virtual bool CanBeRenamed { get; }
```

Determines if the asset can be renamed, override to change this capability.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
#### CanBeSaved
```csharp
public virtual bool CanBeSaved { get; }
```

Determines if the asset can be saved, override to change this capability.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
#### Components
```csharp
public ImmutableDictionary<TKey, TValue> Components { get; }
```

Immutable dictionary of ECS components attached to this character asset.

**Returns** \
[ImmutableDictionary\<TKey, TValue\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableDictionary-2?view=net-7.0) \
#### EditorColor
```csharp
public virtual Vector4 EditorColor { get; }
```

Gets the default color used in the editor for the asset.

**Returns** \
[Vector4](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector4?view=net-7.0) \
#### EditorFolder
```csharp
public virtual string EditorFolder { get; }
```

Gets the folder path in the editor where this asset is grouped.

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
#### FileChanged
```csharp
public bool FileChanged { get; public set; }
```

Indicates whether the asset has unsaved modifications.

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

Unique identifier for this asset, used to reference it from other assets and components.

**Returns** \
[Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \
#### Icon
```csharp
public virtual char Icon { get; }
```

FontAwesome character icon displayed next to this asset in the editor.

**Returns** \
[char](https://learn.microsoft.com/en-us/dotnet/api/System.Char?view=net-7.0) \
#### IsStoredInSaveData
```csharp
public virtual bool IsStoredInSaveData { get; }
```

Whether this file is stored relative to the save path.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
#### Name
```csharp
public string Name { get; public set; }
```

Display name of this asset as shown in the editor.

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
#### Owner
```csharp
public readonly Guid Owner;
```

GUID of the `SpeakerAsset` that represents this character's voice and portrait.

**Returns** \
[Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \
#### Portrait
```csharp
public readonly string Portrait;
```

Portrait which will be shown by default from [CharacterAsset.Owner](../../Murder/Assets/CharacterAsset.html#owner).

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
#### Portraits
```csharp
public ImmutableDictionary<TKey, TValue> Portraits { get; }
```

Named portrait lookup table for the owning `SpeakerAsset`, keyed by portrait identifier.

**Returns** \
[ImmutableDictionary\<TKey, TValue\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableDictionary-2?view=net-7.0) \
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

The folder path where this asset is saved on disk.

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
#### Situations
```csharp
public ImmutableArray<T> Situations { get; }
```

Named dialogue tree lookup for this character, mapping situation names to their `Situation` definitions.

**Returns** \
[ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \
#### StoreInDatabase
```csharp
public virtual bool StoreInDatabase { get; }
```

Whether this asset is stored following the database hierarchy.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
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

Called by the editor when the asset is modified; clears the internal situation and dialogue data caches.

#### Duplicate(string)
```csharp
public GameAsset Duplicate(string name)
```

Creates a deep copy of this asset with the given new name.

**Parameters** \
`name` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

**Returns** \
[GameAsset](../../Murder/Assets/GameAsset.html) \

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

#### TryFetchSituation(int)
```csharp
public T? TryFetchSituation(int id)
```

Attempts to find a dialogue `Situation` by its integer ID; returns null if not found.

**Parameters** \
`id` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

**Returns** \
[T?](https://learn.microsoft.com/en-us/dotnet/api/System.Nullable-1?view=net-7.0) \

#### AfterDeserialized()
```csharp
public virtual void AfterDeserialized()
```

Called after deserialization; rebuilds the internal situation and dialogue data caches.

#### MakeGuid()
```csharp
public void MakeGuid()
```

Generates and assigns a new GUID to this asset.

#### RemoveCustomComponents(IEnumerable<T>)
```csharp
public void RemoveCustomComponents(IEnumerable<T> actionIds)
```

Removes the ECS component override for each of the given dialogue action IDs.

**Parameters** \
`actionIds` [IEnumerable\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Generic.IEnumerable-1?view=net-7.0) \

#### RemoveCustomPortraits(IEnumerable<T>)
```csharp
public void RemoveCustomPortraits(IEnumerable<T> actionIds)
```

Removes the portrait override for each of the given dialogue action IDs.

**Parameters** \
`actionIds` [IEnumerable\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Generic.IEnumerable-1?view=net-7.0) \

#### SetCustomComponentAt(DialogItemId, IComponent)
```csharp
public void SetCustomComponentAt(DialogItemId id, IComponent c)
```

Assigns a custom ECS component override to the specified dialogue line.

**Parameters** \
`id` [DialogItemId](../../Murder/Core/Dialogs/DialogItemId.html) \
`c` [IComponent](../../Bang/Components/IComponent.html) \

#### SetCustomPortraitAt(DialogItemId, Guid, string)
```csharp
public void SetCustomPortraitAt(DialogItemId id, Guid speaker, string portrait)
```

Overrides the speaker and portrait shown on the specified dialogue line.

**Parameters** \
`id` [DialogItemId](../../Murder/Core/Dialogs/DialogItemId.html) \
`speaker` [Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \
`portrait` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### SetSituationAt(int, Situation)
```csharp
public void SetSituationAt(int index, Situation situation)
```

Set the situation on <paramref name="index" /> to <paramref name="situation" />.

**Parameters** \
`index` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`situation` [Situation](../../Murder/Core/Dialogs/Situation.html) \

#### SetSituations(SortedList<TKey, TValue>)
```csharp
public void SetSituations(SortedList<TKey, TValue> situations)
```

Set the situation to a list. 
            This is called when updating the scripts with the latest data.

**Parameters** \
`situations` [SortedList\<TKey, TValue\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Generic.SortedList-2?view=net-7.0) \

#### TrackAssetOnSave(Guid)
```csharp
public void TrackAssetOnSave(Guid g)
```

Queues a dependent asset by GUID to be saved whenever this asset is saved.

**Parameters** \
`g` [Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \



⚡