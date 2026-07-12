# ShowFirstLineAttribute

**Namespace:** Murder.Attributes \
**Assembly:** Murder.dll

```csharp
public class ShowFirstLineAttribute : Attribute
```

Show the first line in the editor.

**Intent:** Tell the editor's custom field for the decorated member to preview only the first line of its text content inline, instead of expanding the full multi-line value.

**Use-case:** Apply to a field whose type is `SituationComponent` (`Murder.Components`) on another component or asset, where showing the whole dialogue body inline would clutter the inspector. `SituationComponentField`, the custom editor field for `SituationComponent`, checks for this attribute on the decorated member and, when present, renders a compact single-line preview of the current dialogue situation instead of the full text.

**Implements:** _[Attribute](https://learn.microsoft.com/en-us/dotnet/api/System.Attribute?view=net-7.0)_

### ⭐ Constructors

```csharp
public ShowFirstLineAttribute()
```

Creates a new instance of `ShowFirstLineAttribute`.

### ⭐ Properties

#### TypeId

```csharp
public virtual Object TypeId { get; }
```

Unique type identifier for this attribute, inherited from `System.Attribute`.

**Returns** \
[Object](https://learn.microsoft.com/en-us/dotnet/api/System.Object?view=net-7.0) \

⚡
