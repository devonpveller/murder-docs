# FadeWhenInCutsceneComponent

**Namespace:** Murder.Components \
**Assembly:** Murder.dll

```csharp
public sealed struct FadeWhenInCutsceneComponent : IComponent
```

Data for gradually fading a sprite's alpha to zero when the entity enters a cutscene, and restoring it afterward. For now, this is only supported for aseprite components.

**Intent:** Carry the fade duration and a snapshot of the sprite's alpha before a cutscene starts, so that a fade-out/fade-in effect can be driven and later reversed. There is currently no system in the engine that consumes this component automatically — attaching it alone will not animate anything; a game-specific system (or a future engine system) is expected to read `Duration`, tween the sprite's alpha to zero, and call `TrackAlpha` to remember the starting value so it can be restored when the cutscene ends.

**Use-case:** If you are building cutscene fade behavior, attach this to an entity you want to hide during cutscenes and write a small system that filters on `FadeWhenInCutsceneComponent` plus a sprite component, uses `Duration` to drive the alpha tween while a cutscene is active, calls `TrackAlpha` to record the alpha before fading starts, and restores `PreviousAlpha` when the cutscene ends.

**Implements:** _[IComponent](../../Bang/Components/IComponent.html)_

### ⭐ Constructors

```csharp
public FadeWhenInCutsceneComponent()
```

Creates a fade-in-cutscene component with no duration and no tracked previous alpha.

```csharp
public FadeWhenInCutsceneComponent(float duration, float previousAlpha)
```

Creates a fade-in-cutscene component with an explicit fade duration and tracked previous alpha.

**Parameters** \
`duration` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`previousAlpha` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

### ⭐ Properties

#### Duration

```csharp
public readonly float Duration;
```

How many seconds the fade transition should take to complete.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### PreviousAlpha

```csharp
public readonly float PreviousAlpha;
```

The entity's alpha value recorded before the cutscene fade began (via `TrackAlpha`), so it can be restored once the cutscene ends. Hidden in the editor and excluded from JSON serialization since it is transient runtime state, not authored data.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

### ⭐ Methods

#### TrackAlpha(float)

```csharp
public FadeWhenInCutsceneComponent TrackAlpha(float alpha)
```

Returns a copy of this component with the given `alpha` recorded as `PreviousAlpha`, used to snapshot the sprite's alpha value at the moment the fade starts so it can later be restored.

**Parameters** \
`alpha` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

**Returns** \
[FadeWhenInCutsceneComponent](../../Murder/Components/FadeWhenInCutsceneComponent.html) \

⚡
