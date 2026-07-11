# EntityBuilder

**Namespace:** Murder.Prefabs \
**Assembly:** Murder.dll

```csharp
public static class EntityBuilder
```

Factory and utility methods for constructing and replacing ECS entities from prefab assets at runtime.

**Intent:** Centralizes the logic for instantiating and hot-swapping entities in the world from `PrefabAsset` definitions.

**Use-case:** Used internally by the engine when placing prefab entities in a world; call `CreateInstance` to build an `EntityInstance` descriptor from a GUID and name without yet spawning it into a world.

### ⭐ Methods
#### CreateInstance(Guid, string, T?)
```csharp
public EntityInstance CreateInstance(Guid assetGuid, string name, T? instanceGuid)
```
Creates an `EntityInstance` descriptor referencing the prefab at `assetGuid`, with the given display name and optional pre-assigned GUID.

**Parameters** \
`assetGuid` [Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \
`name` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
`instanceGuid` [T?](https://learn.microsoft.com/en-us/dotnet/api/System.Nullable-1?view=net-7.0) \

**Returns** \
[EntityInstance](../../Murder/Prefabs/EntityInstance.html) \



⚡