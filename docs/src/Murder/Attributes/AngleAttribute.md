# AngleAttribute

**Namespace:** Murder.Attributes \
**Assembly:** Murder.dll

```csharp
public class AngleAttribute : Attribute
```

An attribute for angle fields. This will show up in the editor
            as a {0, 360} range, but converted in radius in the actual field.

**Intent:** Mark a float field as representing an angle so the editor renders it as a 0–360° degree input widget.

**Use-case:** Apply to float fields in components that store rotation or orientation in radians. Designers see a familiar degree input while the runtime stores the correct radian value automatically.

**Implements:** _[Attribute](https://learn.microsoft.com/en-us/dotnet/api/System.Attribute?view=net-7.0)_

### ⭐ Constructors
```csharp
public AngleAttribute()
```

Creates a new instance of `AngleAttribute`.

### ⭐ Properties
#### TypeId
```csharp
public virtual Object TypeId { get; }
```

Unique type identifier for this attribute, inherited from `System.Attribute`.

**Returns** \
[Object](https://learn.microsoft.com/en-us/dotnet/api/System.Object?view=net-7.0) \


⚡