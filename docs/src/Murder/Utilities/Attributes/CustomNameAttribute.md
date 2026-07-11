# CustomNameAttribute

**Namespace:** Murder.Utilities.Attributes \
**Assembly:** Murder.dll

```csharp
public class CustomNameAttribute : Attribute
```

Overrides the editor display name of a field or component.

**Intent:** Overrides the editor display name of a property or field.

**Use-case:** Apply to a field or component to replace its auto-generated label in the editor with a custom human-readable name.

**Implements:** _[Attribute](https://learn.microsoft.com/en-us/dotnet/api/System.Attribute?view=net-7.0)_

### ⭐ Constructors
```csharp
public CustomNameAttribute(string name)
```

Creates the attribute with the given custom display name.

**Parameters** \
`name` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

### ⭐ Properties
#### Name
```csharp
public string Name;
```

The custom display name that replaces the default auto-generated label.

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
#### TypeId
```csharp
public virtual Object TypeId { get; }
```

Unique object identity for this attribute type, inherited from `Attribute`.

**Returns** \
[Object](https://learn.microsoft.com/en-us/dotnet/api/System.Object?view=net-7.0) \


⚡