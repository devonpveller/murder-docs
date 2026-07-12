# PackedSaveData

**Namespace:** Murder.Assets.Save \
**Assembly:** Murder.dll

```csharp
public class PackedSaveData
```

Wrapper that packages a `SaveData` instance for serialization to a single compressed save file.

**Intent:** Encapsulate the main `SaveData` object so it can be written atomically to `saved.gz` and loaded back without extra ceremony.

**Use-case:** The save system creates a `PackedSaveData` from the active `SaveData` and writes it to disk. Use `SaveDataInfo.GetFullPackedSavePath` to find the file for a given slot and then deserialize `PackedSaveData.Data` to restore game state.

### ⭐ Constructors

```csharp
public PackedSaveData(SaveData data)
```

**Parameters** \
`data` [SaveData](../../../Murder/Assets/SaveData.html) \

### ⭐ Properties

#### Data

```csharp
public readonly SaveData Data;
```

The deserialized `SaveData` payload for this save slot.

**Returns** \
[SaveData](../../../Murder/Assets/SaveData.html) \

#### Name

```csharp
public static const string Name;
```

Filename used when writing this container to disk (`saved.gz`).

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

⚡
