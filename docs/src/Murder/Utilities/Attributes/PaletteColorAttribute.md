# PaletteColorAttribute

**Namespace:** Murder.Utilities.Attributes \
**Assembly:** Murder.dll

```csharp
public class PaletteColorAttribute : Attribute
```

Marks a `Color` field as a palette entry, so the editor shows a color palette picker.

**Intent:** Marks a `Color` field as a palette color reference.

**Use-case:** Apply to a `Color` field to show a palette-color picker in the editor instead of a free color selector.

**Implements:** _[Attribute](https://learn.microsoft.com/en-us/dotnet/api/System.Attribute?view=net-7.0)_

### ⭐ Constructors
```csharp
public PaletteColorAttribute()
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