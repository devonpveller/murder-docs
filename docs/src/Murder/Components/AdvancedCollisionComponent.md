# AdvancedCollisionComponent

**Namespace:** Murder.Components \
**Assembly:** Murder.dll

```csharp
public readonly struct AdvancedCollisionComponent : IComponent
```

Empty marker component with no fields.

**Implements:** _[IComponent](../../Bang/Components/IComponent.html)_

**Intent:** Provides a tag that game code can attach to (and query for) an entity to flag it for some form of non-default collision handling. The engine's built-in physics (`SATPhysicsSystem`) does not currently read this component at all — collision-layer overrides are actually driven by [CustomCollisionMask](../../Murder/Components/CustomCollisionMask.html), which can be attached independently of this one.

**Use-case:** This component ships as an inert marker/reserved extension point. If you need an entity to test against a non-default set of collision layers today, attach [CustomCollisionMask](../../Murder/Components/CustomCollisionMask.html) directly instead. Only reach for `AdvancedCollisionComponent` if you are adding your own game-specific system that filters on it — as shipped, adding or removing it has no observable effect on engine behavior.

⚡
