# NoLabelAttribute

**Namespace:** Murder.Attributes \
**Assembly:** Murder.dll

```csharp
public class NoLabelAttribute : Attribute
```

Suppresses the auto-generated label that the editor renders next to a field widget in the inspector.

**Intent:** Hide the field name label in the editor inspector, rendering only the widget itself.

**Use-case:** Apply to fields whose purpose is self-evident from the widget alone, or to fields in a custom editor layout where an extra label would add unnecessary visual clutter.

**Implements:** _[Attribute](https://learn.microsoft.com/en-us/dotnet/api/System.Attribute?view=net-7.0)_

### ⭐ Constructors
```csharp
public NoLabelAttribute()
```

Creates a new instance of `NoLabelAttribute`.

### ⭐ Properties
#### TypeId
```csharp
public virtual Object TypeId { get; }
```

Unique type identifier for this attribute, inherited from `System.Attribute`.

**Returns** \
[Object](https://learn.microsoft.com/en-us/dotnet/api/System.Object?view=net-7.0) \


⚡