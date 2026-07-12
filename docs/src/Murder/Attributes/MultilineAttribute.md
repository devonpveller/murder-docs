# MultilineAttribute

**Namespace:** Murder.Attributes \
**Assembly:** Murder.dll

```csharp
public class MultilineAttribute : Attribute
```

Marks a string field so the editor renders a multi-line text area widget instead of a single-line input.

**Intent:** Override the default single-line text widget with an expandable multi-line text area for a string field.

**Use-case:** Apply to string fields in components or assets that hold longer text content such as NPC dialogue, item descriptions, or narration blocks, giving designers a more comfortable editing experience.

**Implements:** _[Attribute](https://learn.microsoft.com/en-us/dotnet/api/System.Attribute?view=net-7.0)_

### ⭐ Constructors

```csharp
public MultilineAttribute()
```

Creates a new instance of `MultilineAttribute`.

### ⭐ Properties

#### TypeId

```csharp
public virtual Object TypeId { get; }
```

Unique type identifier for this attribute, inherited from `System.Attribute`.

**Returns** \
[Object](https://learn.microsoft.com/en-us/dotnet/api/System.Object?view=net-7.0) \

⚡
