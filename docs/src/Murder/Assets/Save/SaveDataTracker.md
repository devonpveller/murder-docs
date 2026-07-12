# SaveDataTracker

**Namespace:** Murder.Assets.Save \
**Assembly:** Murder.dll

```csharp
public class SaveDataTracker
```

Top-level registry that tracks all available save slots with their version and display-name metadata.

**Intent:** Provide a single serialized index of every save slot so the game can enumerate them quickly without loading the full `PackedSaveData` for each slot.

**Use-case:** Serialize a `SaveDataTracker` to `save_data.gz` at the root of the save directory. At startup read `Data` to populate the save-select screen; use each `SaveDataInfo` entry to verify versions and show slot names before loading a full `PackedSaveData`. Override `OnBeforeSave` in a game-specific subclass to run custom logic (e.g. pruning stale slots) right before the tracker is written to disk.

### ⭐ Constructors

```csharp
public SaveDataTracker()
```

Creates an empty tracker (`Data` starts as `ImmutableDictionary<int, SaveDataInfo>.Empty`). Slots are added later via `Data`'s immutable-dictionary APIs as saves are created.

### ⭐ Properties

#### Data

```csharp
public ImmutableDictionary<TKey, TValue> Data;
```

Maps each save slot index to its `SaveDataInfo` metadata (version and display name). This is the field that actually gets serialized to `save_data.gz`; read it at startup to populate a save-select screen without loading each slot's full `PackedSaveData`.

**Returns** \
[ImmutableDictionary\<TKey, TValue\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableDictionary-2?view=net-7.0) \

#### Name

```csharp
public static const string Name;
```

Filename used when writing the tracker to disk (`save_data.gz`).

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

### ⭐ Methods

#### OnBeforeSave()

```csharp
public virtual void OnBeforeSave()
```

Called by the save system immediately before the tracker is serialized to disk. Does nothing by default; override in a game-specific subclass to run custom logic (e.g. validation or cleanup) right before the save-slot index is persisted.

⚡
