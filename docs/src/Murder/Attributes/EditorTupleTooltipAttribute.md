# EditorTupleTooltipAttribute

**Namespace:** Murder.Attributes \
**Assembly:** Murder.dll

```csharp
public class EditorTupleTooltipAttribute : Attribute
```

Tooltip that will show up when hovering over a field in the editor.

**Intent:** Attach separate tooltip strings to each element of a two-value (tuple or pair) field in the editor inspector.

**Use-case:** Apply to tuple or vector fields in components where each element has a distinct semantic meaning—for example annotating a `(min, max)` range with "Minimum value" and "Maximum value" respectively.

**Implements:** _[Attribute](https://learn.microsoft.com/en-us/dotnet/api/System.Attribute?view=net-7.0)_

### ⭐ Constructors
```csharp
public EditorTupleTooltipAttribute(string tooltip1, string tooltip2)
```

Creates a new instance with tooltip text for each element of the decorated tuple or pair field.

**Parameters** \
`tooltip1` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
`tooltip2` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

### ⭐ Properties
#### Tooltip1
```csharp
public string Tooltip1;
```

The content of the tooltip.

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
#### Tooltip2
```csharp
public string Tooltip2;
```

The content of the tooltip.

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
#### TypeId
```csharp
public virtual Object TypeId { get; }
```

Unique type identifier for this attribute, inherited from `System.Attribute`.

**Returns** \
[Object](https://learn.microsoft.com/en-us/dotnet/api/System.Object?view=net-7.0) \


⚡