# RequiresVisionComponent

**Namespace:** Murder.Components \
**Assembly:** Murder.dll

```csharp
public sealed struct RequiresVisionComponent : IComponent
```

Marker component gating an entity's visual representation behind the player's field of vision.

**Intent:** Hide an entity's visual representation until the player's vision/perception covers it.

**Use-case:** Attach to secrets, hidden enemies, or fog-of-war-gated scenery. This is a hook for game-specific fog-of-war/line-of-sight rendering systems to filter on — the engine does not ship a built-in system that acts on it, so a project must implement the actual vision-gated rendering logic. It shares the same notion of "vision" as [HasVisionComponent](../../Murder/Components/HasVisionComponent.html), which marks entities (typically AI agents) as able to perceive others.

**Implements:** _[IComponent](../../Bang/Components/IComponent.html)_

### ⭐ Properties

#### OnlyOnce

```csharp
public readonly bool OnlyOnce;
```

When true, once the entity has been seen at least once it remains visible/rendered from then on (a "fog of war reveals permanently" behavior). When false, the entity should hide again as soon as it leaves the observer's vision.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

⚡
