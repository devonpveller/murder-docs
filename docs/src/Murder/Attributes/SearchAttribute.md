# SearchAttribute

**Namespace:** Murder.Attributes \
**Assembly:** Murder.dll

```csharp
public class SearchAttribute : Attribute
```

Allow EnumFields to be searchable.

**Intent:** Mark an enum-typed field so the editor renders it as a searchable/filterable dropdown instead of the default plain combo box.

**Use-case:** Apply to enum fields whose values are easier to find by typing than by scrolling — the editor's `EnumField` custom field already switches to the searchable widget automatically once an enum has more than 10 values, so this attribute is mainly useful to opt a smaller enum into the same search UI, as seen on the keyboard/gamepad binding fields in `InputInformation` (`src/Murder/Assets/Input/InputProfileAsset.cs`).

**Implements:** _[Attribute](https://learn.microsoft.com/en-us/dotnet/api/System.Attribute?view=net-7.0)_

### ⭐ Constructors

```csharp
public SearchAttribute()
```

Creates a new instance of `SearchAttribute`.

### ⭐ Properties

#### TypeId

```csharp
public virtual Object TypeId { get; }
```

Unique type identifier for this attribute, inherited from `System.Attribute`.

**Returns** \
[Object](https://learn.microsoft.com/en-us/dotnet/api/System.Object?view=net-7.0) \

⚡
