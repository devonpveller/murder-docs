# TagsComponent

**Namespace:** Murder.Components.Utilities \
**Assembly:** Murder.dll

```csharp
public sealed struct TagsComponent : IComponent
```

Attaches a set of gameplay tags to an entity, used by physics and AI systems to categorise or filter entities.

**Intent:** Store a compact tag bitmask on an entity for fast category-based queries (e.g. collision layer filtering or movement modifier checks).

**Use-case:** Attach to any entity that needs to participate in tag-based queries; set `Tags` to the appropriate flag combination for that entity's category.

**Implements:** _[IComponent](../../../Bang/Components/IComponent.html)_

### ⭐ Properties
#### Tags
```csharp
public readonly Tags Tags;
```

Bitmask of gameplay tags assigned to this entity.

**Returns** \
[Tags](../../../Murder/Core/Tags.html) \


⚡