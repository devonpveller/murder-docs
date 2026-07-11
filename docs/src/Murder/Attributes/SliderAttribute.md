# SliderAttribute

**Namespace:** Murder.Attributes \
**Assembly:** Murder.dll

```csharp
public class SliderAttribute : Attribute
```

A slider attribute used when setting values in the editor.

**Intent:** Render a numeric field as a bounded slider widget in the editor inspector.

**Use-case:** Apply to float or int fields that represent values within a known range, such as volume (0–1), movement speed (0–10), or opacity (0–255), to give designers an intuitive drag-based input instead of a raw number box.

**Implements:** _[Attribute](https://learn.microsoft.com/en-us/dotnet/api/System.Attribute?view=net-7.0)_

### ⭐ Constructors
```csharp
public SliderAttribute(float minimum, float maximum)
```

Creates a new [SliderAttribute](../../Murder/Attributes/SliderAttribute.html).

**Parameters** \
`minimum` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
\
`maximum` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
\

### ⭐ Properties
#### Maximum
```csharp
public readonly float Maximum;
```

Maximum value.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
#### Minimum
```csharp
public readonly float Minimum;
```

Minimum value.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
#### TypeId
```csharp
public virtual Object TypeId { get; }
```

Unique type identifier for this attribute, inherited from `System.Attribute`.

**Returns** \
[Object](https://learn.microsoft.com/en-us/dotnet/api/System.Object?view=net-7.0) \


⚡