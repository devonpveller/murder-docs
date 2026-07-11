# HighlightOnChildrenComponent

**Namespace:** Murder.Components \
**Assembly:** Murder.dll

```csharp
public sealed struct HighlightOnChildrenComponent : IComponent
```

Component that specifies that any highlight should be applied on the children (instead of self).

**Intent:** Redirect highlight effects (such as `HighlightSpriteComponent`) from the parent entity to all of its children.

**Use-case:** Add to a composite entity (e.g. a multi-part character or door) so that hovering or selecting it highlights the child sprites rather than the root entity.

**Implements:** _[IComponent](../../Bang/Components/IComponent.html)_



⚡