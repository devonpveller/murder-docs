# FontAttribute

**Namespace:** Murder.Utilities.Attributes \
**Assembly:** Murder.dll

```csharp
public class FontAttribute : Attribute
```

Marks an integer field as a font index reference, so the editor shows a font-picker dropdown.

**Intent:** Marks an integer field as a font index.

**Use-case:** Apply to an int field in a component so the editor shows a font-picker dropdown instead of a raw integer input.

**Implements:** _[Attribute](https://learn.microsoft.com/en-us/dotnet/api/System.Attribute?view=net-7.0)_

### ⭐ Constructors
```csharp
public FontAttribute()
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