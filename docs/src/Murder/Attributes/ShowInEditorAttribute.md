# ShowInEditorAttribute

**Namespace:** Murder.Attributes \
**Assembly:** Murder.dll

```csharp
public class ShowInEditorAttribute : Attribute
```

Marks a field or property so it is exposed in the editor inspector and, when the field is non-public, also included when the field is written out to JSON.
Commonly used for private fields.

**Intent:** Force a non-public field to appear in the editor inspector even though it would normally be hidden due to its access modifier, and simultaneously opt it into JSON serialization.

**Use-case:** Apply to private or protected fields in components where designers need direct inspector access for gameplay tuning, without changing the field's access level in code. By default the inspector only reflects public members (with a few special-cased exceptions, such as state machine components), and the JSON serializer only persists private fields carrying `[Serialize]`; `ShowInEditorAttribute` is checked alongside `[Serialize]` in `SerializationHelper` so a field tagged with it is both visible in the editor and round-tripped through save/asset files without also being marked `[Serialize]`.

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
