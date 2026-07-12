# GuidId

**Namespace:** Murder.Components \
**Assembly:** Murder.dll

```csharp
public sealed struct GuidId
```

A named GUID pair used as an entry in `GuidToIdTargetCollectionComponent.Collection`, associating a human-readable name (`Id`) with a target entity's design-time instance GUID (`Target`). This lets level authors reference other entities by name; at load time the serializer resolves `Target` to a live runtime entity id.

**Intent:** Store a human-readable name alongside an entity GUID so that a single `GuidToIdTargetCollectionComponent` can carry several named references, and each can be looked up by name via `GuidToIdTargetCollectionComponent.TryFindGuid`.

**Use-case:** Used as entries in `GuidToIdTargetCollectionComponent` to map named targets (e.g. `"door"`, `"enemy_spawn"`) to their corresponding entity GUIDs; the engine's world-loading step (`WorldProcessor`) resolves each entry's `Target` into a runtime entity id and stores the result in an `IdTargetCollectionComponent`.

### ⭐ Constructors

```csharp
public GuidId()
```

Creates an empty entry with a blank id and default target GUID.

```csharp
public GuidId(string id, Guid target)
```

Creates an entry associating the name `id` with the entity GUID `target`.

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

The design-time instance GUID of the referenced entity, resolved to a runtime entity id when the world loads.

**Returns** \
[Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \

⚡
