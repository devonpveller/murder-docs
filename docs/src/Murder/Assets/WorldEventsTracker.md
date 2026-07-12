# WorldEventsTracker

**Namespace:** Murder.Assets \
**Assembly:** Murder.dll

```csharp
public static class WorldEventsTracker
```

Static entry point that runs every `WorldEventsAsset`'s `Preprocess` against a newly created `World`.

**Intent:** Decouple world-creation code from having to know about every `WorldEventsAsset` in the game -- it looks the full set up once (cached) and runs each one's preprocessing step against the world being built.

**Use-case:** Call `PreprocessWorldEvents` once when a world is set up (as `WorldAsset.CreateInstance` does) so all global event watchers get the chance to register themselves in that world. Call `ClearCache` after `WorldEventsAsset` instances are added, removed, or reloaded (e.g. hot-reload in the editor) so the next preprocessing pass picks up the change.

### ⭐ Methods

#### PreprocessWorldEvents(World, CreateWorldFlags)

```csharp
public static void PreprocessWorldEvents(World world, CreateWorldFlags flags)
```

Runs `WorldEventsAsset.Preprocess` for every `WorldEventsAsset` in the game's asset database against `world`. The set of `WorldEventsAsset`s is looked up once and cached until `ClearCache` is called.

**Parameters** \
`world` [World](../../Bang/World.html) \
`flags` [CreateWorldFlags](../../Murder/Assets/CreateWorldFlags.html) \

#### ClearCache()

```csharp
public static void ClearCache()
```

Discards the cached list of `WorldEventsAsset`s, forcing the next call to `PreprocessWorldEvents` to re-query the asset database.

⚡
