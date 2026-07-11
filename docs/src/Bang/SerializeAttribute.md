# SerializeAttribute

**Namespace:** Bang \
**Assembly:** Bang.dll

```csharp
public sealed class SerializeAttribute : Attribute
```

Indicates that the property or field should be included for serialization and deserialization.

When applied to a public property, indicates that non-public getters and setters should be used for
serialization and deserialization. This supports non-public properties or fields, which is why this is
used instead of [System.Text.Json.Serialization.JsonIncludeAttribute](https://learn.microsoft.com/en-us/dotnet/api/System.Text.Json.Serialization.JsonIncludeAttribute?view=net-7.0).

It may be applied to properties or fields only (not classes, methods, etc.) and cannot be applied more than
once to the same member.

**Implements:** _[Attribute](https://learn.microsoft.com/en-us/dotnet/api/System.Attribute?view=net-7.0)_

### ⭐ Constructors
```csharp
public SerializeAttribute()
```

Initializes a new instance of [SerializeAttribute](../Bang/SerializeAttribute.html).

### ⭐ Properties
#### TypeId
```csharp
public virtual Object TypeId { get; }
```

**Returns** \
[Object](https://learn.microsoft.com/en-us/dotnet/api/System.Object?view=net-7.0) \


⚡