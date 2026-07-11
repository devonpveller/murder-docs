# IRenderSystem

**Namespace:** Bang.Systems \
**Assembly:** Bang.dll

```csharp
public abstract IRenderSystem : ISystem
```

A system that leverages the engine implementations of render functionality, i.e. it
            draws things to the screen rather than mutating game state. Bang itself does not define
            a render method on this interface - the concrete signature (e.g. taking a render context
            or graphics batch) is supplied by the game/engine layer built on top of Bang. Systems that
            implement [IRenderSystem](../../Bang/Systems/IRenderSystem.html) are never automatically deactivated by
            [World.Pause](../../Bang/World.html), since the world keeps rendering the (frozen) game state while
            paused; if a render system should stop drawing while paused, it must handle that itself
            (e.g. by checking [World.IsPaused](../../Bang/World.html)).

**Implements:** _[ISystem](../../Bang/Systems/ISystem.html)_



⚡
