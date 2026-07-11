# DoNotPersistEntityOnSaveAttribute

**Namespace:** Murder.Attributes \
**Assembly:** Murder.dll

```csharp
public class DoNotPersistEntityOnSaveAttribute : Attribute
```

This signalizes that an entity should be skipped altogether if
            it has a component with that attribute.

**Intent:** Exclude an entire entity from save-game serialization when any of its components carries this attribute.

**Use-case:** Apply to transient or runtime-only components (such as temporary visual effects, particle emitters, or UI entities) so their owning entities are never written to the save file.

**Implements:** _[Attribute](https://learn.microsoft.com/en-us/dotnet/api/System.Attribute?view=net-7.0)_

### ⭐ Constructors
```csharp
public DoNotPersistEntityOnSaveAttribute()
```

Creates a new instance of `DoNotPersistEntityOnSaveAttribute`.

### ⭐ Properties
#### TypeId
```csharp
public virtual Object TypeId { get; }
```

Unique type identifier for this attribute, inherited from `System.Attribute`.

**Returns** \
[Object](https://learn.microsoft.com/en-us/dotnet/api/System.Object?view=net-7.0) \


⚡