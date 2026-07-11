# IntrinsicAttribute

**Namespace:** Murder.Attributes \
**Assembly:** Murder.dll

```csharp
public class IntrinsicAttribute : Attribute
```

This signalizes that a component is an intrinsic characteristic of the entity and 
            that it does not distinct as a separate entity.
            An entity with only intrinsic components will not be serialized.

**Intent:** Declare that a component is an inseparable trait of its owning entity and should not be treated as independently meaningful persistent state.

**Use-case:** Apply to foundational components like `Transform` or `EntityName` that every entity is expected to have. Entities composed only of such components are omitted from save files because they represent no standalone game state.

**Implements:** _[Attribute](https://learn.microsoft.com/en-us/dotnet/api/System.Attribute?view=net-7.0)_

### ⭐ Constructors
```csharp
public IntrinsicAttribute()
```

Creates a new instance of `IntrinsicAttribute`.

### ⭐ Properties
#### TypeId
```csharp
public virtual Object TypeId { get; }
```

Unique type identifier for this attribute, inherited from `System.Attribute`.

**Returns** \
[Object](https://learn.microsoft.com/en-us/dotnet/api/System.Object?view=net-7.0) \


⚡