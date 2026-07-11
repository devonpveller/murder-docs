# ShowInEditorAttribute

**Namespace:** Murder.Attributes \
**Assembly:** Murder.dll

```csharp
public class ShowInEditorAttribute : Attribute
```

Attributes for fields that should always show up in the editor.
            Commonly used for private fields.

**Intent:** Force a field to appear in the editor inspector even if it would normally be hidden due to its access modifier.

**Use-case:** Apply to private or protected fields in components where designers need direct inspector access for gameplay tuning, without changing the field's access level in code.

**Implements:** _[Attribute](https://learn.microsoft.com/en-us/dotnet/api/System.Attribute?view=net-7.0)_

### ⭐ Constructors
```csharp
public ShowInEditorAttribute()
```

Creates a new instance of `ShowInEditorAttribute`.

### ⭐ Properties
#### TypeId
```csharp
public virtual Object TypeId { get; }
```

Unique type identifier for this attribute, inherited from `System.Attribute`.

**Returns** \
[Object](https://learn.microsoft.com/en-us/dotnet/api/System.Object?view=net-7.0) \


⚡