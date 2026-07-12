# TagsComponent

**Namespace:** Murder.Components.Utilities \
**Assembly:** Murder.dll

```csharp
public sealed struct TagsComponent : IComponent
```

Attaches a compact bitmask of gameplay category tags to an entity, so systems can filter or match entities by category without depending on their specific component composition.

**Implements:** _[IComponent](../../../Bang/Components/IComponent.html)_

**Intent:** Provide a generic, cheap "does this entity belong to category X" check that any system can use. Currently used by `AgentMovementModifierSystem`, which checks a movement-modifier area's `AffectOnly` [Tags](../../../Murder/Core/Tags.html) value against an actor's `TagsComponent` (via `Tags.HasTags`) to decide whether that area (e.g. mud, ice, a conveyor) should affect the actor at all.

**Use-case:** Attach to any entity that needs to opt in or out of tag-based gameplay rules; set `Tags` to the appropriate flag combination for that entity's category (or leave it as the default "matches everything" `Tags` value if the entity should be affected by every tag-filtered rule).

### ⭐ Properties

#### Tags

```csharp
public readonly Tags Tags;
```

Bitmask of gameplay category tags assigned to this entity, checked with `Tags.HasTag`/`Tags.HasTags`-style comparisons by systems that filter entities by category.

**Returns** \
[Tags](../../../Murder/Core/Tags.html) \

⚡
