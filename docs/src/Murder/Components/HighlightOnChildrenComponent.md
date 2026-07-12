# HighlightOnChildrenComponent

**Namespace:** Murder.Components \
**Assembly:** Murder.dll

```csharp
public sealed struct HighlightOnChildrenComponent : IComponent
```

Component that specifies that any highlight (`HighlightSpriteComponent`) should be applied on the children of this entity, rather than the entity itself. Consumed by `EffectsServices.ApplyHighlight` and `EffectsServices.RemoveHighlight`, which route the highlight to `Child` (if set) or to every child of the entity's root otherwise.

**Intent:** Let composite entities (e.g. multi-part characters or doors) whose visible parts are separate child sprites redirect a highlight effect to the correct child sprite(s) instead of the (often invisible) root entity.

**Use-case:** Add to a composite entity so that hovering over or targeting it highlights the child sprites rather than the root entity; set `Child` to redirect the highlight to one specific named child, or leave it `null` to highlight every child of the entity's root.

**Implements:** _[IComponent](../../Bang/Components/IComponent.html)_

### ⭐ Constructors

```csharp
public HighlightOnChildrenComponent()
```

Redirects highlighting to all children of this entity's root.

### ⭐ Properties

#### Child

```csharp
public readonly string? Child;
```

Name of the single child to highlight, as registered via `Entity.AddChild`. When `null`, the highlight is instead applied to every child of the entity's root.

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

⚡
