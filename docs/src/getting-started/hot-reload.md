# Asset Hot-Reloading

The Murder editor supports hot-reloading of all asset types — ECS asset JSON files, images, fonts, shaders, localization, and dialogue. When enabled, any changes you make to asset files on disk are automatically detected and reloaded into the editor the next time the editor window regains focus — no manual rebuild required.

This mirrors Unity's batched import workflow: changes accumulate asynchronously, then are processed in a single non-blocking pipeline when the editor is brought back into focus.

## Enabling Hot-Reload

Hot-reload is controlled by the `AutomaticallyHotReloadAssets` setting in [`EditorSettingsAsset`](../Murder/Editor/Assets/EditorSettingsAsset.html). Set it to `true` to enable:

```csharp
EditorSettings.AutomaticallyHotReloadAssets = true;
```

When enabled, the editor initializes a file system watcher on both asset directories:

- `assets/data/` — generic assets (prefabs, characters, etc.)
- `assets/ecs/` — content ECS assets (worlds, tilesets, etc.)

## How It Works

### 1. Change Detection

A [`FileSystemWatcher`](https://learn.microsoft.com/en-us/dotnet/api/system.io.filesystemwatcher) monitors the asset directories for changes across all supported formats: `.json` (ECS assets), `.png` (sprites), `.aseprite`/`.ase` (Aseprite animations), `.ttf` (fonts), `.fx` (shaders), `.csv` (localization), and `.gum` (dialogue). Paths are accumulated in two thread-safe sets — **changed** paths (modified or deleted files) and **created** paths (new files or renames) — so the refresh pipeline can distinguish between updating existing assets and discovering new ones. No processing happens during the file events themselves.

### 2. Metadata Cache

On startup, the editor builds an in-memory cache of all loaded assets, recording each asset's disk `LastWriteTime` and `FileSize`. It also walks every `AssetRef<T>` field and property via reflection to build a **dependency graph**: if asset A references asset B, then B is a dependency of A, and A is a dependent of B.

### 3. Dirty Propagation

When the editor regains focus, it compares cached timestamps against disk. Any asset whose timestamp has changed is marked dirty. The dirty flag then propagates through the dependency graph via BFS — if a sprite asset changes, every prefab that references it is also marked dirty. Cycle detection prevents infinite loops.

### 4. Phased Reload

Assets are reloaded in dependency order to ensure referenced assets are available before their consumers:

1. **Native assets** — `FontAsset`, `SpriteAsset`
2. **Prefabs** — `PrefabAsset`
3. **Worlds** — `WorldAsset`
4. **Remaining types** — any other asset types not in the explicit order

Each asset is deserialized from disk, removed from the database, and re-added. The metadata cache is rebuilt after the full cycle completes.

### 5. New Asset Discovery

After the phased reload, the pipeline scans the **created paths** set for any `.json` files not yet in the asset database. Each new file is deserialized, added to the database (with duplicate GUID handling), and registered in the metadata cache. This means newly created asset files appear in the editor automatically on the next focus cycle — no manual import step needed.

### 6. Non-JSON Resource Reimport

Any non-JSON files (images, fonts, shaders, etc.) that changed or were created trigger the resource importer pipeline. This re-processes affected sprites, fonts, and shaders through the same importers used during initial content load, ensuring all asset types stay in sync.

### 7. Loading Overlay

While a refresh cycle is in progress, the editor displays a semi-transparent overlay with an animated spinner and "Refreshing assets..." text. This provides visual feedback that background work is happening and signals the user to wait before interacting with the UI.

### 8. Error Handling

Individual asset failures (corrupt JSON, missing files) are logged and skipped — they never abort the entire refresh cycle. Deleted files are cleanly removed from the database. Failed new-asset deserialization is logged as a warning and skipped.

## Triggering a Refresh

Hot-reload fires automatically when the editor window regains focus and there are pending file changes. You can also trigger it manually by calling:

```csharp
EditorDataManager.ToggleHotReloadAssets(true);
```

This is useful for enabling/disabling hot-reload at runtime without restarting the editor.

## Performance

The refresh pipeline is fully async and uses [`PerfTimeRecorder`](../Murder/Diagnostics/PerfTimeRecorder.html) to time each phase. Large batches of changes are processed in a single cycle, keeping UI responsive.
