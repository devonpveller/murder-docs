# PrefabRefComponent

**Namespace:** Murder.Components \
**Assembly:** Murder.dll

```csharp
public sealed struct PrefabRefComponent : IComponent
```

Tags an entity with the [PrefabAsset](../../Murder/Assets/PrefabAsset.html) it was instantiated from.

**Intent:** Let a runtime entity be traced back to the design-time prefab asset it came from, without needing to inspect its components or naming.

**Use-case:** Added automatically by [EntityBuilder](../../Murder/Prefabs/EntityBuilder.html) whenever an entity is created from a `PrefabAsset` (as opposed to being assembled ad-hoc in code). Editor and debug tooling read it to show a friendly asset name for an entity (see `EntityServices.TryGetEntityName`), and gameplay code can use it via `AssetServices.GetAsset`/`TryGetAsset` to fetch the original prefab data at runtime.

**Implements:** _[IComponent](../../Bang/Components/IComponent.html)_

### ⭐ Constructors

```csharp
public PrefabRefComponent(Guid assetGui)
```

Creates a component that references the prefab asset identified by `assetGui`. Called by `EntityBuilder` when an entity is instantiated from a prefab; game code rarely needs to construct this directly.

**Parameters** \
`assetGui` [Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \

### ⭐ Properties

#### AssetGuid

```csharp
public readonly Guid AssetGuid;
```

GUID of the [PrefabAsset](../../Murder/Assets/PrefabAsset.html) this entity was instantiated from. Pass this to `Game.Data.GetAsset<PrefabAsset>` (or use the `GetAsset`/`TryGetAsset` extension methods on this component) to look up the source asset.

**Returns** \
[Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \

⚡
