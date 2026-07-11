# RuntimeOnlyAttribute

**Namespace:** Murder.Utilities.Attributes \
**Assembly:** Murder.dll

```csharp
public class RuntimeOnlyAttribute : Attribute
```

This is an attribute for components which will not be added during with
            an editor in saved world or asset, but rather dynamically added in runtime.

**Intent:** Marks a component as runtime-only so it is never serialized or saved.

**Use-case:** Apply to components that are created and destroyed dynamically at runtime and must not appear in the editor or saved asset files.

**Implements:** _[Attribute](https://learn.microsoft.com/en-us/dotnet/api/System.Attribute?view=net-7.0)_

### ⭐ Constructors
```csharp
public RuntimeOnlyAttribute()
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