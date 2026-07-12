# PrefabReference

**Namespace:** Murder.Prefabs \
**Assembly:** Murder.dll

```csharp
public sealed struct PrefabReference
```

Lightweight wrapper around a `PrefabAsset` GUID that resolves the actual asset lazily through `Game.Data`.

**Intent:** Avoids threading a raw `Guid` through `PrefabEntityInstance` and re-resolving it by hand every time the backing prefab is needed; `Fetch()`/`CanFetch` centralize that lookup (and the null/missing-asset check) in one place.

**Use-case:** `PrefabEntityInstance.PrefabRef` is a `PrefabReference` pointing at the prefab the instance was placed from; every override in `PrefabEntityInstance` (components, children, activation state) is expressed as a delta on top of `PrefabRef.Fetch()`. Check `CanFetch` before calling `Fetch()` in editor or tooling code where the referenced asset may have been deleted or not yet loaded, since `Fetch()` throws when the asset cannot be found.

### ⭐ Constructors

```csharp
public PrefabReference(Guid guid)
```

Creates a new reference to the prefab asset identified by `guid`.

**Parameters** \
`guid` [Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \

### ⭐ Properties

#### CanFetch

```csharp
public bool CanFetch { get; }
```

Returns `true` if the referenced `PrefabAsset` GUID is loaded and can be fetched.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### Guid

```csharp
public readonly Guid Guid;
```

Reference to a [PrefabAsset](../../Murder/Assets/PrefabAsset.html).

**Returns** \
[Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \

### ⭐ Methods

#### Fetch()

```csharp
public PrefabAsset Fetch()
```

Loads and returns the `PrefabAsset` this reference points to; throws if the asset is not found.

**Returns** \
[PrefabAsset](../../Murder/Assets/PrefabAsset.html) \

⚡
