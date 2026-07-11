# PrefabRefComponent

**Namespace:** Murder.Components \
**Assembly:** Murder.dll

```csharp
public sealed struct PrefabRefComponent : IComponent
```

Stores a reference to the prefab asset that this entity was originally created from.

**Intent:** Track the originating prefab GUID so the engine can map a runtime entity back to its source asset.

**Use-case:** Added automatically when the engine instantiates a prefab; use it to identify or reload prefab data at runtime.

**Implements:** _[IComponent](../../Bang/Components/IComponent.html)_

### ⭐ Constructors
```csharp
public PrefabRefComponent(Guid assetGui)
```

**Parameters** \
`assetGui` [Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \

### ⭐ Properties
#### AssetGuid
```csharp
public readonly Guid AssetGuid;
```

GUID of the prefab asset this entity was instantiated from.

**Returns** \
[Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \


⚡