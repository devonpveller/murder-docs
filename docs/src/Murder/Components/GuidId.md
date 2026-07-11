# GuidId

**Namespace:** Murder.Components \
**Assembly:** Murder.dll

```csharp
public sealed struct GuidId
```

A named GUID pair used to associate a string identifier with a target entity's instance GUID.

**Intent:** Store a human-readable name alongside an entity GUID so that serialized references can be looked up by name at runtime.

**Use-case:** Used as entries in `GuidToIdTargetCollectionComponent` to map named targets (e.g. `"door"`, `"enemy_spawn"`) to their corresponding entity GUIDs.

### ⭐ Constructors
```csharp
public GuidId()
```

```csharp
public GuidId(string id, Guid target)
```

**Parameters** \
`id` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
`target` [Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \

### ⭐ Properties
#### Id
```csharp
public readonly string Id;
```

Human-readable string identifier used to look up this entry by name.

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
#### Target
```csharp
public readonly Guid Target;
```

The instance GUID of the entity this entry references.

**Returns** \
[Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \


⚡