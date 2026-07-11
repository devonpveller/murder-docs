# ChildIdAttribute

**Namespace:** Murder.Utilities.Attributes \
**Assembly:** Murder.dll

```csharp
public class ChildIdAttribute : Attribute
```

Attribute for string fields that point to an entity child id.

**Intent:** Marks an integer field as a child entity ID slot.

**Use-case:** Apply to an int field in a component so the editor displays a child entity picker instead of a raw integer input.

**Implements:** _[Attribute](https://learn.microsoft.com/en-us/dotnet/api/System.Attribute?view=net-7.0)_

### ⭐ Constructors
```csharp
public ChildIdAttribute()
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