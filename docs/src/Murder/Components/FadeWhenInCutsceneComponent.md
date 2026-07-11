# FadeWhenInCutsceneComponent

**Namespace:** Murder.Components \
**Assembly:** Murder.dll

```csharp
public sealed struct FadeWhenInCutsceneComponent : IComponent
```

For now, this is only supported for aseprite components.

**Intent:** Gradually fade a sprite's alpha to zero (or a target value) when the entity enters a cutscene.

**Use-case:** Attach to any entity that should smoothly disappear during cutscene playback; the system reads `Duration` to drive the tween and restores the original alpha via `PreviousAlpha` when the cutscene ends.

**Implements:** _[IComponent](../../Bang/Components/IComponent.html)_

### ⭐ Constructors
```csharp
public FadeWhenInCutsceneComponent()
```

```csharp
public FadeWhenInCutsceneComponent(float duration, float previousAlpha)
```

**Parameters** \
`duration` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`previousAlpha` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

### ⭐ Properties
#### Duration
```csharp
public readonly float Duration;
```

How many seconds the fade animation should take to complete.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
#### PreviousAlpha
```csharp
public readonly float PreviousAlpha;
```

The entity's alpha value before the cutscene fade began, used to restore the sprite on cutscene exit. Hidden in the editor.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
### ⭐ Methods
#### TrackAlpha(float)
```csharp
public FadeWhenInCutsceneComponent TrackAlpha(float alpha)
```

Returns a copy of this component with the given `alpha` recorded as `PreviousAlpha`, used by the system to snapshot the current alpha at fade start.

**Parameters** \
`alpha` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

**Returns** \
[FadeWhenInCutsceneComponent](../../Murder/Components/FadeWhenInCutsceneComponent.html) \



⚡