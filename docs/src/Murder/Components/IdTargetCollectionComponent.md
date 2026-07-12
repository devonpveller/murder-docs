# IdTargetCollectionComponent

**Namespace:** Murder.Components \
**Assembly:** Murder.dll

```csharp
public sealed struct IdTargetCollectionComponent : IComponent
```

The runtime counterpart of `GuidToIdTargetCollectionComponent`: holds a named collection of live entity ids resolved by `WorldProcessor.PostProcessEntitiesFirstTime` when the world is instantiated. Marked `[RuntimeOnly]` since it only exists after resolution, `[PersistOnSave]` so the resolved references survive a save, and `[KeepOnReplace]` so replacing the entity's components does not drop these references.

**Intent:** Store a named set of runtime entity id references so that systems can look up multiple target entities by string key, once the design-time GUID references have been resolved to actual entity ids.

**Use-case:** Attached automatically by `WorldProcessor` after resolving `GuidToIdTargetCollectionComponent`; read `Targets` (case-insensitive by name) to find the live entity ids associated with each named reference authored in the editor.

**Implements:** _[IComponent](../../Bang/Components/IComponent.html)_

### ⭐ Constructors

```csharp
public IdTargetCollectionComponent(ImmutableDictionary<string, int> targets)
```

Creates the component from an already-built name-to-entity-id dictionary.

**Parameters** \
`targets` [ImmutableDictionary\<string, int\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableDictionary-2?view=net-7.0) \

```csharp
public IdTargetCollectionComponent(string id, int target)
```

Creates the component with a single named target entity.

**Parameters** \
`id` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
`target` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

```csharp
public IdTargetCollectionComponent(string id1, int target1, string id2, int target2)
```

Creates the component with two named target entities.

**Parameters** \
`id1` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
`target1` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`id2` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
`target2` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

### ⭐ Properties

#### Targets

```csharp
public readonly ImmutableDictionary<string, int> Targets;
```

Maps each named reference (case-insensitively) to the runtime entity id it resolved to.

**Returns** \
[ImmutableDictionary\<string, int\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableDictionary-2?view=net-7.0) \

⚡
