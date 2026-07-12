# EditorFieldFlags

**Namespace:** Murder.Attributes \
**Assembly:** Murder.dll

```csharp
public sealed enum EditorFieldFlags : Enum, IComparable, ISpanFormattable, IFormattable, IConvertible
```

Bitwise flags that control how a field is rendered and filtered inside the Murder editor inspector.

**Intent:** Provide composable display options for the `EditorFieldPropertiesAttribute` to fine-tune field widget behavior.

**Use-case:** Combine flags in `[EditorFieldProperties(EditorFieldFlags.SingleLine | EditorFieldFlags.NoFilter)]` to control whether the inspector shows filter controls or forces a field onto a single line.

**Implements:** _[Enum](https://learn.microsoft.com/en-us/dotnet/api/System.Enum?view=net-7.0), [IComparable](https://learn.microsoft.com/en-us/dotnet/api/System.IComparable?view=net-7.0), [ISpanFormattable](https://learn.microsoft.com/en-us/dotnet/api/System.ISpanFormattable?view=net-7.0), [IFormattable](https://learn.microsoft.com/en-us/dotnet/api/System.IFormattable?view=net-7.0), [IConvertible](https://learn.microsoft.com/en-us/dotnet/api/System.IConvertible?view=net-7.0)_

### ⭐ Properties

#### NoFilter

```csharp
public static const EditorFieldFlags NoFilter;
```

Disables the search/filter widget for this field's contents in the editor inspector.

**Returns** \
[EditorFieldFlags](../../Murder/Attributes/EditorFieldFlags.html) \

#### None

```csharp
public static const EditorFieldFlags None;
```

No special editor behavior applied; uses the default field rendering.

**Returns** \
[EditorFieldFlags](../../Murder/Attributes/EditorFieldFlags.html) \

#### SingleLine

```csharp
public static const EditorFieldFlags SingleLine;
```

Forces the field widget to render on a single line in the inspector instead of expanding to multiple lines.

**Returns** \
[EditorFieldFlags](../../Murder/Attributes/EditorFieldFlags.html) \

⚡
