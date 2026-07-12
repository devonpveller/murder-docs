# EditorLabelAttribute

**Namespace:** Murder.Attributes \
**Assembly:** Murder.dll

```csharp
public class EditorLabelAttribute : Attribute
```

Label that will show up for this field in the editor.

**Intent:** Override the auto-generated field label displayed next to a widget in the editor inspector.

**Use-case:** Apply to component fields whose C# identifier is not self-explanatory in a design context. For tuple or pair fields, provide two labels to annotate each element separately, such as labeling a `(float, float)` pair as "Min" and "Max".

**Implements:** _[Attribute](https://learn.microsoft.com/en-us/dotnet/api/System.Attribute?view=net-7.0)_

### ⭐ Constructors

```csharp
public EditorLabelAttribute(string label1, string label2)
```

Creates a new instance with two labels for annotating both elements of a pair or tuple field.

**Parameters** \
`label1` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
`label2` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

```csharp
public EditorLabelAttribute(string label1)
```

Creates a new instance with a single label for the decorated field.

**Parameters** \
`label1` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

### ⭐ Properties

#### Label1

```csharp
public readonly string Label1;
```

The content of the tooltip.

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### Label2

```csharp
public readonly string Label2;
```

[Optional] Secondary label.

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
