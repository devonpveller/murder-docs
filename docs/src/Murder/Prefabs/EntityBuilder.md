# EntityBuilder

**Namespace:** Murder.Prefabs \
**Assembly:** Murder.dll

```csharp
public static class EntityBuilder
```

Internal factory and mutation logic that turns `EntityInstance`/`PrefabEntityInstance` descriptors into live `Entity` objects inside a `World`, and that replaces an existing `Entity` in-place with the contents of a prefab.

**Intent:** This is the low-level engine plumbing behind `EntityInstance.Create`, `PrefabEntityInstance.Create` and `PrefabAsset.Create`/`Replace`. It deep-copies any `IModifiableComponent` so that multiple instances of the same prefab never share mutable component state, attaches a `PrefabRefComponent` so the spawned entity remembers which asset it came from, recursively spawns children (respecting `EntityModifier` overrides), and post-processes a handful of editor-only "shortcut" components (event listeners, speaker listeners, sprite-facing overrides) into their runtime equivalents before the entity is considered ready.

**Use-case:** Game code and gameplay systems never call the `Create`/`Replace` methods on this class directly — they are `internal` and only reachable through `EntityInstance.Create(World, ...)`, `PrefabEntityInstance.Create(World, ...)`, or `PrefabAsset.Create`/`Replace`. The one method exposed to the rest of the engine is `CreateInstance`, which is how `PrefabAsset.ToInstance`/`ToInstanceAsAsset` and `ParticleSystemAsset` build a fresh `EntityInstance` (or `PrefabEntityInstance`, when `assetGuid` is not `Guid.Empty`) descriptor without touching a `World` at all — useful when you need an instance object to hand to the editor or to another asset before anything is actually spawned.

### ⭐ Methods

#### CreateInstance(Guid, string, Guid)

```csharp
public static EntityInstance CreateInstance(Guid assetGuid, string? name = default, Guid? instanceGuid = null)
```

Builds a standalone `EntityInstance` descriptor without spawning anything into a `World`. When `assetGuid` is `Guid.Empty` this returns a plain `EntityInstance` with no prefab backing; otherwise it returns a `PrefabEntityInstance` bound to the prefab at `assetGuid`, using `instanceGuid` as its identity if provided (a new `Guid` is generated otherwise). This is the method `PrefabAsset.ToInstance`/`ToInstanceAsAsset` call to turn an existing prefab asset into a fresh, independent instance, and what `ParticleSystemAsset` uses to seed a `PrefabAsset` wrapper for an emitted particle's entity template.

**Parameters** \
`assetGuid` [Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \
`name` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
`instanceGuid` [Guid?](https://learn.microsoft.com/en-us/dotnet/api/System.Nullable-1?view=net-7.0) \

**Returns** \
[EntityInstance](../../Murder/Prefabs/EntityInstance.html) \

⚡
