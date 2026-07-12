# AssetServices

**Namespace:** *(none — declared in the global namespace)* \
**Assembly:** Murder.dll

```csharp
public static class AssetServices
```

Helpers for instantiating and replacing entities from `PrefabAsset` GUIDs. Unlike every other class in this folder, `AssetServices` has no `namespace` declaration in its source file and therefore lives in the C# global namespace rather than `Murder.Services` — callers can use it without a `using Murder.Services;` import.

**Intent:** Wraps the two-step "resolve the `PrefabAsset` for a GUID, then create/replace an entity from it" pattern that would otherwise be repeated at every prefab-instantiation call site across the engine and game code.

**Use-case:** Call `Create`/`TryCreate` to spawn an entity from a prefab GUID (e.g. a bullet, pickup, or enemy prefab authored in the editor) into a `World`. Use `ReplaceEntity` to re-run a prefab's component setup onto an already-existing entity (e.g. hot-reloading a prefab's definition onto its live instances). Use the `PrefabRefComponent` extension overloads of `GetAsset`/`TryGetAsset` to go from an entity that already has a `PrefabRefComponent` back to the `PrefabAsset` it was created from.

### ⭐ Methods

#### Create(World, Guid)

```csharp
public static Entity Create(World world, Guid guid)
```

Creates an entity from the `PrefabAsset` identified by `guid` and adds it to `world`, returning the *top-level* entity — if the created entity has a parent (some prefabs create a hierarchy), the parent is returned instead of the child. Throws an `InvalidStateMachineException` (and logs a fatal error) if the asset can't be resolved or entity creation otherwise fails. Prefer this over `TryCreate` when a missing/invalid GUID represents a bug that should fail loudly rather than be handled gracefully.

**Parameters** \
`world` [World](../../Bang/World.html) \
`guid` [Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \

**Returns** \
[Entity](../../Bang/Entities/Entity.html) \

#### TryCreate(World, Guid)

```csharp
public static Entity? TryCreate(World world, Guid guid)
```

Creates an entity from the `PrefabAsset` identified by `guid` and adds it to `world`, returning `null` (instead of throwing) if the asset can't be resolved or the created entity can't be found in `world` afterward. This is the safe counterpart to `Create`, and the one used internally by `EntityServices.Spawn` and similar call sites where a missing prefab shouldn't crash the game.

**Parameters** \
`world` [World](../../Bang/World.html) \
`guid` [Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \

**Returns** \
[Entity](../../Bang/Entities/Entity.html) \

#### ReplaceEntity(World, Entity, Guid)

```csharp
public static bool ReplaceEntity(World world, Entity e, Guid guid)
```

Re-applies the `PrefabAsset` identified by `guid` onto the already-existing entity `e` (via `PrefabAsset.Replace`), rebuilding its components to match the prefab's current definition in place rather than creating a brand-new entity. Returns `false` if the asset can't be resolved. Useful for editor-driven "apply changes" workflows or hot-reloading a prefab definition onto entities that already reference it.

**Parameters** \
`world` [World](../../Bang/World.html) \
`e` [Entity](../../Bang/Entities/Entity.html) \
`guid` [Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### GetAsset(Guid)

```csharp
public static PrefabAsset GetAsset(Guid guid)
```

Returns the `PrefabAsset` identified by `guid`, asserting it exists (via `Game.Data.GetAsset<PrefabAsset>`). Use when the asset is expected to always be present and a missing one should surface as an error.

**Parameters** \
`guid` [Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \

**Returns** \
[PrefabAsset](../../Murder/Assets/PrefabAsset.html) \

#### TryGetAsset(Guid)

```csharp
public static PrefabAsset? TryGetAsset(Guid guid)
```

Returns the `PrefabAsset` identified by `guid`, or `null` if it doesn't exist.

**Parameters** \
`guid` [Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \

**Returns** \
[PrefabAsset](../../Murder/Assets/PrefabAsset.html) \

#### GetAsset(PrefabRefComponent)

```csharp
public static PrefabAsset GetAsset(this PrefabRefComponent component)
```

Extension method that resolves the `PrefabAsset` referenced by a `PrefabRefComponent`'s `AssetGuid`, asserting it exists. Use `entity.GetPrefabRef().GetAsset()` to go from an already-instantiated entity back to the prefab it came from.

**Parameters** \
`component` [PrefabRefComponent](../../Murder/Components/PrefabRefComponent.html) \

**Returns** \
[PrefabAsset](../../Murder/Assets/PrefabAsset.html) \

#### TryGetAsset(PrefabRefComponent)

```csharp
public static PrefabAsset? TryGetAsset(this PrefabRefComponent component)
```

Extension method that resolves the `PrefabAsset` referenced by a `PrefabRefComponent`'s `AssetGuid`, or `null` if it can't be found.

**Parameters** \
`component` [PrefabRefComponent](../../Murder/Components/PrefabRefComponent.html) \

**Returns** \
[PrefabAsset](../../Murder/Assets/PrefabAsset.html) \

⚡
