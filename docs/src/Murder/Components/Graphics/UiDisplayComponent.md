# UiDisplayComponent

**Namespace:** Murder.Components.Graphics \
**Assembly:** Murder.dll

```csharp
public sealed struct UiDisplayComponent : IComponent
```

Marks an entity to be rendered in the UI layer, with an optional Y-axis sorting offset.

**Intent:** Ensure an entity is drawn as part of the UI rather than the gameplay world layer, and control its sort order within that layer.

**Use-case:** Add to HUD or overlay entities that should always render on top of the world; set `YSort` to fine-tune their draw order relative to other UI elements.

**Implements:** _[IComponent](../../../Bang/Components/IComponent.html)_

### ⭐ Constructors
```csharp
public UiDisplayComponent()
```

### ⭐ Properties
#### YSort
```csharp
public readonly float YSort;
```

Sorting offset applied within the UI layer to control draw order relative to other UI entities.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \


⚡