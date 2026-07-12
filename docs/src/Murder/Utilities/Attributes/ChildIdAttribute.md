# ChildIdAttribute

**Namespace:** Murder.Utilities.Attributes \
**Assembly:** Murder.dll

```csharp
public class ChildIdAttribute : Attribute
```

Marks a [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) field as a reference to the id of a child of the currently selected entity.

**Intent:** Lets a component field point at one of the selected entity's children by name, with editor support for picking a valid one.

**Use-case:** Apply to a `string` field in a component such as `BroadcastEventMessageComponent` or `ChildTargetComponent` so the editor's string field shows a combo box populated from the selected entity's children (`StageHelpers.GetChildNamesForSelectedEntity`) instead of a free-text box, avoiding a mistyped child id that would fail to resolve at runtime.

**Implements:** _[Attribute](https://learn.microsoft.com/en-us/dotnet/api/System.Attribute?view=net-7.0)_

### ⭐ Constructors

```csharp
public ChildIdAttribute()
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
