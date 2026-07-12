# PauseAnimationComponent

**Namespace:** Murder.Components \
**Assembly:** Murder.dll

```csharp
public sealed struct PauseAnimationComponent : IComponent
```

Marker component that exempts an entity's sprite animation from being paused: while attached, `SpriteRenderSystem` evaluates the animation using unscaled time (`Game.NowUnscaled`) instead of scaled game time, so it keeps advancing even while the game is paused or `TimeScale` is set to 0.

**Intent:** Let specific entities (e.g. UI elements, pause-menu decorations, or effects that must keep playing through a pause) continue animating normally regardless of the game's pause/time-scale state.

**Use-case:** Add to an entity whose animation must never freeze — for example a pause-menu cursor or background flourish — so it keeps looping while the rest of the world is paused; remove the component to have it follow scaled game time like everything else.

**Implements:** _[IComponent](../../Bang/Components/IComponent.html)_

⚡
