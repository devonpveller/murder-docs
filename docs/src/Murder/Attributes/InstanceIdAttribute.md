# InstanceIdAttribute

**Namespace:** Murder.Attributes \
**Assembly:** Murder.dll

```csharp
public class InstanceIdAttribute : Attribute
```

This is an attribute used for a field guid that points to another entity instance within the world.

**Intent:** Mark a `Guid` field as a reference to a specific entity instance placed in the current world, enabling the editor to display an entity instance picker.

**Use-case:** Apply to `Guid` fields in components that cross-reference other entities in the scene, such as a “target door” or “spawn point” reference. The editor will show a list of named entity instances from the current world rather than a raw GUID input.

**Implements:** _[Attribute](https://learn.microsoft.com/en-us/dotnet/api/System.Attribute?view=net-7.0)_

### ⭐ Constructors

```csharp
public InstanceIdAttribute()
```

Creates a new instance of `InstanceIdAttribute`.

### ⭐ Properties

#### TypeId

```csharp
public virtual Object TypeId { get; }
```

Unique type identifier for this attribute, inherited from `System.Attribute`.

**Returns** \
[Object](https://learn.microsoft.com/en-us/dotnet/api/System.Object?view=net-7.0) \

⚡
