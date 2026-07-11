# SaveDataInfo

**Namespace:** Murder.Assets.Save \
**Assembly:** Murder.dll

```csharp
public class SaveDataInfo
```

Lightweight metadata record for a save slot, storing the save version and display name without loading the full save payload.

**Intent:** Let the game list available save slots and check version compatibility before committing to a full deserialization of the packed save files.

**Use-case:** Stored in `SaveDataTracker.Info` keyed by slot number. Read `SaveDataInfo.Version` to verify the save was created with a compatible game version, and `SaveDataInfo.Name` to display the slot label in a save/load menu.

### ⭐ Constructors
```csharp
public SaveDataInfo(float version, string name)
```

**Parameters** \
`version` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`name` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

### ⭐ Properties
#### Name
```csharp
public string Name;
```

User-facing display name of this save slot (e.g. the in-game save name chosen by the player).

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
#### Version
```csharp
public float Version;
```

Game version number recorded when the save was created, used for compatibility checks.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
### ⭐ Methods
#### GetFullPackedAssetsSavePath(int)
```csharp
public string GetFullPackedAssetsSavePath(int slot)
```

Returns the full file path for the packed assets save file (`saved_assets.gz`) for the given slot.

**Parameters** \
`slot` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### GetFullPackedSaveDirectory(int)
```csharp
public string GetFullPackedSaveDirectory(int slot)
```

Returns the directory path that contains all save files for the given slot number.

**Parameters** \
`slot` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### GetFullPackedSavePath(int)
```csharp
public string GetFullPackedSavePath(int slot)
```

Returns the full file path for the main packed save file (`saved.gz`) for the given slot.

**Parameters** \
`slot` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \



⚡