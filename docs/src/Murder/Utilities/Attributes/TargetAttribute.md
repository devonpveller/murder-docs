# TargetAttribute

**Namespace:** Murder.Utilities.Attributes \
**Assembly:** Murder.dll

```csharp
public class TargetAttribute : Attribute
```

Attribute for string fields that are actually targets of the entity.

**Intent:** Marks a field as an entity target reference.

**Use-case:** Apply to a string or int field in a component so the editor shows an entity-picker that lets the designer select a named target entity.

**Implements:** _[Attribute](https://learn.microsoft.com/en-us/dotnet/api/System.Attribute?view=net-7.0)_

### ⭐ Constructors
```csharp
public TargetAttribute()
```

### ⭐ Properties
#### TypeId
```csharp
public virtual Object TypeId { get; }
```

Unique object identity for this attribute type, inherited from `Attribute`.

**Returns** \
[Object](https://learn.microsoft.com/en-us/dotnet/api/System.Object?view=net-7.0) \


⚡