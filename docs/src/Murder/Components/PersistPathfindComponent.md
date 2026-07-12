# PersistPathfindComponent

**Namespace:** Murder.Components \
**Assembly:** Murder.dll

```csharp
public sealed struct PersistPathfindComponent : IComponent
```

Marker component that opts a [RouteComponent](../../Murder/Components/RouteComponent.html) into persistence across save/load cycles. Normally a computed pathfinding route is discarded on save; attaching this component preserves it.

**Intent:** Keep a computed pathfinding route alive when the world is serialised.

**Use-case:** Attach alongside [RouteComponent](../../Murder/Components/RouteComponent.html) on any agent that must resume its current path after the game is saved and reloaded.

**Implements:** _[IComponent](../../Bang/Components/IComponent.html)_

⚡
