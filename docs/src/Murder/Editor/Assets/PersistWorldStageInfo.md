# PersistWorldStageInfo

**Namespace:** Murder.Editor.Assets \
**Assembly:** Murder.dll

```csharp
public readonly struct PersistWorldStageInfo
```

Persisted entity-group visibility state for a single world asset's editor view.

**Intent:** The world editor lets a developer organize entities into named groups and hide or lock them from selection while working on a scene (e.g. to focus on gameplay entities without background decoration getting in the way); this struct remembers which groups were hidden/locked so that state survives closing and reopening the world.

**Use-case:** Stored in [EditorSettingsAsset.WorldAssetInfo](../../../Murder/Editor/Assets/EditorSettingsAsset.html#worldassetinfo) keyed by the world's GUID. Written by `WorldAssetEditor_Selector.SavePersistentWorldInfo` whenever the developer changes group visibility/lock state, and read back when the world editor reopens that world to restore the same groups as hidden/locked.

### ⭐ Constructors

```csharp
public PersistWorldStageInfo(HashSet<string> lockedGroups, HashSet<string> hiddenGroups)
```

Creates a snapshot of which entity groups were locked and hidden in a world editor session.

**Parameters** \
`lockedGroups` [HashSet\<string\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Generic.HashSet-1?view=net-7.0) -- names of entity groups excluded from selection. \
`hiddenGroups` [HashSet\<string\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Generic.HashSet-1?view=net-7.0) -- names of entity groups excluded from rendering. \

### ⭐ Properties

#### HiddenGroups

```csharp
public readonly HashSet<string> HiddenGroups { get; init; }
```

Names of entity groups that were hidden (not rendered) in the world editor.

**Returns** \
[HashSet\<string\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Generic.HashSet-1?view=net-7.0) \

#### LockedGroups

```csharp
public readonly HashSet<string> LockedGroups { get; init; }
```

Names of entity groups that were locked (excluded from selection) in the world editor.

**Returns** \
[HashSet\<string\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Generic.HashSet-1?view=net-7.0) \

⚡
