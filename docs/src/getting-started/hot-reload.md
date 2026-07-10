# Asset Hot-Reloading

The Murder editor supports hot-reloading of ECS asset JSON files. When enabled, any changes you make to asset files on disk are automatically detected and reloaded into the editor the next time the editor window regains focus — no manual rebuild required.

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

A [`FileSystemWatcher`](https://learn.microsoft.com/en-us/dotnet/api/system.io.filesystemwatcher) monitors the asset directories for `.json` file changes (create, modify, delete, rename). Changed paths are accumulated in a thread-safe set — no processing happens during the file events themselves.

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

### 5. Error Handling

Individual asset failures (corrupt JSON, missing files) are logged and skipped — they never abort the entire refresh cycle. Deleted files are cleanly removed from the database.

## Triggering a Refresh

Hot-reload fires automatically when the editor window regains focus and there are pending file changes. You can also trigger it manually by calling:

```csharp
EditorDataManager.ToggleHotReloadAssets(true);
```

This is useful for enabling/disabling hot-reload at runtime without restarting the editor.

## Performance

The refresh pipeline is fully async and uses [`PerfTimeRecorder`](../Murder/Diagnostics/PerfTimeRecorder.html) to time each phase. Large batches of changes are processed in a single cycle, keeping UI responsive.
