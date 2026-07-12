# EditorFieldPropertiesAttribute

**Namespace:** Murder.Attributes \
**Assembly:** Murder.dll

```csharp
public class EditorFieldPropertiesAttribute : Attribute
```

Configures additional display properties for a field in the Murder editor inspector using `EditorFieldFlags`.

**Intent:** Customize how an individual field is rendered in the editor inspector by supplying one or more display flag options.

**Use-case:** Apply to component fields to override default inspector widget behavior—for example to disable the filter widget on a list field or force a string to render on a single line.

**Implements:** _[Attribute](https://learn.microsoft.com/en-us/dotnet/api/System.Attribute?view=net-7.0)_

### ⭐ Constructors

```csharp
public EditorFieldPropertiesAttribute(EditorFieldFlags flags)
```

Creates a new instance with the specified display flags applied to the decorated field.

**Parameters** \
`flags` [EditorFieldFlags](../../Murder/Attributes/EditorFieldFlags.html) \

### ⭐ Properties

#### Flags

```csharp
public EditorFieldFlags Flags;
```

The set of `EditorFieldFlags` that control how the decorated field is rendered in the inspector.

**Returns** \
[EditorFieldFlags](../../Murder/Attributes/EditorFieldFlags.html) \

#### TypeId

```csharp
public virtual Object TypeId { get; }
```

Unique type identifier for this attribute, inherited from `System.Attribute`.

**Returns** \
[Object](https://learn.microsoft.com/en-us/dotnet/api/System.Object?view=net-7.0) \

⚡
