# HideInEditorAttribute

**Namespace:** Murder.Attributes \
**Assembly:** Murder.dll

```csharp
public class HideInEditorAttribute : Attribute
```

Marks a field or property so it is hidden from the Murder editor inspector and not displayed to designers.

**Intent:** Suppress a specific field from appearing in the editor inspector to keep the UI clean.

**Use-case:** Apply to internal implementation-detail fields in components that designers should not see or modify directly, such as cached computed values or internal state flags.

**Implements:** _[Attribute](https://learn.microsoft.com/en-us/dotnet/api/System.Attribute?view=net-7.0)_

### ⭐ Constructors
```csharp
public HideInEditorAttribute()
```

Creates a new instance of `HideInEditorAttribute`.

### ⭐ Properties
#### TypeId
```csharp
public virtual Object TypeId { get; }
```

Unique type identifier for this attribute, inherited from `System.Attribute`.

**Returns** \
[Object](https://learn.microsoft.com/en-us/dotnet/api/System.Object?view=net-7.0) \


⚡