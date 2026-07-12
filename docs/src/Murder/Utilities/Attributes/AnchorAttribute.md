# AnchorAttribute

**Namespace:** Murder.Utilities.Attributes \
**Assembly:** Murder.dll

```csharp
public class AnchorAttribute : Attribute
```

Marks a [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) field as a reference to a named anchor within the currently selected cutscene/state machine.

**Intent:** Lets a component field point at a state machine anchor by name, with editor support for picking a valid one.

**Use-case:** Apply to a `string` field in a component so the editor's string field renders a combo box populated from the anchors available on the selected cutscene entity (`StageHelpers.GetAnchorNamesForSelectedEntity`) instead of a free-text box, preventing typos in anchor names that would otherwise fail to resolve silently at runtime.

**Implements:** _[Attribute](https://learn.microsoft.com/en-us/dotnet/api/System.Attribute?view=net-7.0)_

### ⭐ Constructors

```csharp
public AnchorAttribute()
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
