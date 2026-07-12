# AnimationEventsTriggerFlag

**Namespace:** Murder.Components.Graphics \
**Assembly:** Murder.dll

```csharp
public sealed enum AnimationEventsTriggerFlag : Enum, IComparable, ISpanFormattable, IFormattable, IConvertible
```

Flags controlling how `RenderServices.TriggerEventsIfNeeded` matches sprite animation frame-events against the frames the animation has advanced through since the last check.

**Intent:** Animation frame events (named triggers authored on specific frames of an aseprite animation, e.g. a footstep or hit-frame marker) are normally only fired as the animation advances forward in time. Ratio-driven sprites (see [ForceSpriteDrawAtRatioComponent](../../../Murder/Components/ForceSpriteDrawAtRatioComponent.html)) can move their frame backward as well as forward, so `SpriteAtRatioRenderSystem` passes `AllowReverse` to also fire events when scrubbing backward through frames; the default, time-driven render systems (`SpriteRenderSystem`, `AgentSpriteSystem`) pass `None` since their frame index only ever increases within an animation.

**Use-case:** Passed as the last argument to `RenderServices.TriggerEventsIfNeeded` by the sprite render systems; game code does not typically construct this directly.

**Implements:** _[Enum](https://learn.microsoft.com/en-us/dotnet/api/System.Enum?view=net-7.0), [IComparable](https://learn.microsoft.com/en-us/dotnet/api/System.IComparable?view=net-7.0), [ISpanFormattable](https://learn.microsoft.com/en-us/dotnet/api/System.ISpanFormattable?view=net-7.0), [IFormattable](https://learn.microsoft.com/en-us/dotnet/api/System.IFormattable?view=net-7.0), [IConvertible](https://learn.microsoft.com/en-us/dotnet/api/System.IConvertible?view=net-7.0)_

### ⭐ Properties

#### AllowReverse

```csharp
public static const AnimationEventsTriggerFlag AllowReverse;
```

Also trigger events when the animation frame moves backwards (e.g. a reversed or ping-ponging animation).

**Returns** \
[AnimationEventsTriggerFlag](../../../Murder/Components/Graphics/AnimationEventsTriggerFlag.html) \

#### None

```csharp
public static const AnimationEventsTriggerFlag None;
```

No special handling; only forward frame advances trigger events.

**Returns** \
[AnimationEventsTriggerFlag](../../../Murder/Components/Graphics/AnimationEventsTriggerFlag.html) \

⚡
