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

#### GetFullPackedAssetsSavePath(int, string)

```csharp
public static string GetFullPackedAssetsSavePath(int slot, string? basepath = null)
```

Returns the full file path for the packed assets save file (`saved_assets.gz`) for the given slot. Static helper used by the save/load pipeline to locate the file on disk; pass `basepath` to override `Game.Data.SaveBasePath` (mainly used for testing or exporting saves to a custom location).

**Parameters** \
`slot` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`basepath` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### GetFullPackedSaveDirectory(int, string)

```csharp
public static string GetFullPackedSaveDirectory(int slot, string? basePath = null)
```

Returns the directory path that contains all save files for the given slot number (i.e. `<basePath>/<slot>`). Static helper used whenever the save system needs to enumerate or create the on-disk folder for a slot.

**Parameters** \
`slot` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`basePath` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### GetFullPackedSaveBackupDirectory(int)

```csharp
public static string GetFullPackedSaveBackupDirectory(int slot)
```

Returns the directory path used to store a backup copy of a save slot's files (`<SaveBasePath>/<slot>/backup`), always rooted at `Game.Data.SaveBasePath`. Used by the save system before overwriting a slot's files, so a corrupted write can be recovered from the backup.

**Parameters** \
`slot` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### GetFullPackedSavePath(int, string)

```csharp
public static string GetFullPackedSavePath(int slot, string? basepath = null)
```

Returns the full file path for the main packed save file (`saved.gz`) for the given slot. Static helper used by the save/load pipeline to locate the file on disk; pass `basepath` to override `Game.Data.SaveBasePath`.

**Parameters** \
`slot` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`basepath` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

⚡
