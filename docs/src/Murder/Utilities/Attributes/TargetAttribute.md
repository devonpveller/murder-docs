# TargetAttribute

**Namespace:** Murder.Utilities.Attributes \
**Assembly:** Murder.dll

```csharp
public class TargetAttribute : Attribute
```

Marks a [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) field as a reference to a named "guid target" registered on the currently selected entity.

**Intent:** Lets a component field point at a target registered via `GuidToIdTargetComponent`/`GuidToIdTargetCollectionComponent`, with editor support for picking a valid one instead of typing its name.

**Use-case:** Apply to a `string` field in a component/interaction, such as `DeactivateChildForTargetInteraction` or `EnableChildrenInteraction`, so the editor's string field shows a combo box populated from the selected entity's registered targets (`StageHelpers.GetTargetNamesForSelectedEntity`) instead of a free-text box, avoiding a mistyped target name that would fail to resolve at runtime.

**Implements:** _[Attribute](https://learn.microsoft.com/en-us/dotnet/api/System.Attribute?view=net-7.0)_

### ⭐ Constructors

```csharp
public TargetAttribute()
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
