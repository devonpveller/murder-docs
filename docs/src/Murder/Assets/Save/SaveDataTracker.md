# SaveDataTracker

**Namespace:** Murder.Assets.Save \
**Assembly:** Murder.dll

```csharp
public sealed struct SaveDataTracker
```

Top-level registry that tracks all available save slots with their version and display-name metadata.

**Intent:** Provide a single serialized index of every save slot so the game can enumerate them quickly without loading the full `PackedSaveData` for each slot.

**Use-case:** Serialize a `SaveDataTracker` to `save_data.gz` at the root of the save directory. At startup read `Info` to populate the save-select screen; use `SaveDataInfo` values to verify versions and show slot names before loading a full `PackedSaveData`.

### ⭐ Constructors
```csharp
public SaveDataTracker(Dictionary<TKey, TValue> info)
```

**Parameters** \
`info` [Dictionary\<TKey, TValue\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Generic.Dictionary-2?view=net-7.0) \

### ⭐ Properties
#### Info
```csharp
public readonly Dictionary<TKey, TValue> Info;
```

Dictionary mapping save slot indices to their `SaveDataInfo` metadata records.

**Returns** \
[Dictionary\<TKey, TValue\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Generic.Dictionary-2?view=net-7.0) \
#### Name
```csharp
public static const string Name;
```

Filename used when writing the tracker to disk (`save_data.gz`).

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \


⚡