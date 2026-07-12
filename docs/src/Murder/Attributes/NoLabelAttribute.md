# NoLabelAttribute

**Namespace:** Murder.Attributes \
**Assembly:** Murder.dll

```csharp
public class NoLabelAttribute : Attribute
```

Marker attribute intended to tag a field whose value is self-descriptive enough that the inspector's auto-generated name label next to it is unnecessary.

**Intent:** Flag a field so its widget can be drawn without the usual "FieldName:" label prefix, for cases where the label would be redundant.

**Use-case:** The engine applies this to `AddComponentOnInteraction.Component`, a field that already embeds a full component picker/editor whose contents make an extra "Component:" label superfluous. Reach for it on similarly self-explanatory single-value fields.

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
