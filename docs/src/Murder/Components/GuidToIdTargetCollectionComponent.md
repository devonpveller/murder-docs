# GuidToIdTargetCollectionComponent

**Namespace:** Murder.Components \
**Assembly:** Murder.dll

```csharp
public sealed struct GuidToIdTargetCollectionComponent : IComponent
```

This is a component used to translate entity instaces guid to an actual entity id.

**Intent:** Persist multiple named GUID-to-entity-ID mappings at design time so they can be resolved to runtime entity IDs when the world is loaded.

**Use-case:** Add to an entity that needs to reference several other entities by name; the serialization system automatically translates each `GuidId` in `Collection` into the corresponding runtime `IdTargetCollectionComponent`.

**Implements:** _[IComponent](../../Bang/Components/IComponent.html)_

### ⭐ Constructors
```csharp
public GuidToIdTargetCollectionComponent()
```

### ⭐ Properties
#### Collection
```csharp
public readonly ImmutableArray<T> Collection;
```

Guid of the target entity.

**Returns** \
[ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \
### ⭐ Methods
#### TryFindGuid(string)
```csharp
public T? TryFindGuid(string name)
```

Searches the collection for a `GuidId` entry whose `Id` matches `name` (case-insensitive) and returns its target `Guid`, or `null` if not found.

**Parameters** \
`name` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

**Returns** \
[T?](https://learn.microsoft.com/en-us/dotnet/api/System.Nullable-1?view=net-7.0) \



⚡