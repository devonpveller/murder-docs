# SpriteBatchReferenceAttribute

**Namespace:** Murder.Utilities.Attributes \
**Assembly:** Murder.dll

```csharp
public class SpriteBatchReferenceAttribute : Attribute
```

Marks an integer field as a sprite batch layer reference.

**Intent:** Marks an integer field as a sprite batch layer reference.

**Use-case:** Apply to an int field in a component so the editor shows a batch layer picker instead of a raw integer.

**Implements:** _[Attribute](https://learn.microsoft.com/en-us/dotnet/api/System.Attribute?view=net-7.0)_

### ⭐ Constructors
```csharp
public SpriteBatchReferenceAttribute()
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