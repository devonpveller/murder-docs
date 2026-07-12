# HideInEditorAttribute

**Namespace:** Murder.Attributes \
**Assembly:** Murder.dll

```csharp
public class HideInEditorAttribute : Attribute
```

Marks a component, asset, state machine, or field/property so it is excluded from the Murder editor.

**Intent:** Filter a type or member out of the editor entirely, whether that means removing a whole component/asset/state-machine type from search boxes and creation menus, or hiding a single field from the auto-generated inspector.

**Use-case:** When applied to a type, `HideInEditorAttribute` removes it from reflection-driven pickers such as the "add component" search box, the asset creation menu, and state machine selection dialogs (checked via `ReflectionHelper.GetAllImplementationsOf` and the filters in `AssetsFilter`). This is used for base/internal component and asset types that should never be added or selected directly by a designer. When applied to a field or property, it is excluded from the reflected member list used to draw the inspector, letting a member stay public in code (so other code can use it) while still being kept out of the designer-facing UI.

**Implements:** _[Attribute](https://learn.microsoft.com/en-us/dotnet/api/System.Attribute?view=net-7.0)_

### ⭐ Constructors

```csharp
public HideInEditorAttribute()
```

Creates a new instance of `HideInEditorAttribute`.

### ⭐ Properties

#### TypeId

```csharp
public virtual Object TypeId { get; }
```

Unique type identifier for this attribute, inherited from `System.Attribute`.

**Returns** \
[Object](https://learn.microsoft.com/en-us/dotnet/api/System.Object?view=net-7.0) \

⚡
