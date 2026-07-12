# DefaultAttribute

**Namespace:** Murder.Attributes \
**Assembly:** Murder.dll

```csharp
public class DefaultAttribute : Attribute
```

Text which will be displayed when a field has a default value.

**Intent:** Provide a human-readable button label for creating or resetting a field to its default value in the editor inspector.

**Use-case:** Apply to a field or type to replace the generic “create default” button text with a context-specific label, such as “Add New Waypoint”, making the editor more intuitive for designers.

**Implements:** _[Attribute](https://learn.microsoft.com/en-us/dotnet/api/System.Attribute?view=net-7.0)_

### ⭐ Constructors

```csharp
public DefaultAttribute(string text)
```

Creates a new [DefaultAttribute](../../Murder/Attributes/DefaultAttribute.html).

**Parameters** \
`text` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
\

### ⭐ Properties

#### Text

```csharp
public string Text;
```

The content which will be displayed in the button to create a new value of the default field.

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
