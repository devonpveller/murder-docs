# PrefabReference

**Namespace:** Murder.Prefabs \
**Assembly:** Murder.dll

```csharp
public sealed struct PrefabReference
```

Represents an entity placed on the map.

**Intent:** Holds a GUID reference to a `PrefabAsset` so it can be instantiated at runtime.

**Use-case:** Store in a component field to reference a prefab that should be spawned dynamically; use `CanFetch` before calling fetch methods.

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