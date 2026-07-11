# AnimationInfo

**Namespace:** Murder.Core.Graphics \
**Assembly:** Murder.dll

```csharp
public sealed struct AnimationInfo
```

Encapsulates the playback parameters used to evaluate a sprite animation each frame.

**Intent:** Carries the clip name, start time, loop flag, and timing mode needed to look up the correct animation frame without storing mutable state.

**Use-case:** Pass an `AnimationInfo` to sprite-rendering helpers (e.g., `NineSliceInfo.Draw`, `CachedNineSlice.Draw`) to control which animation plays and whether it loops.

### ⭐ Constructors
```csharp
public AnimationInfo()
```

Creates an `AnimationInfo` with default values (empty name, looping, unscaled time).

```csharp
public AnimationInfo(string name, float start)
```

**Parameters** \
`name` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
`start` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

```csharp
public AnimationInfo(string name)
```

**Parameters** \
`name` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

### ⭐ Properties
#### Default
```csharp
public readonly static AnimationInfo Default;
```

A ready-made `AnimationInfo` with all default settings (empty name, looping, unscaled time).

**Returns** \
[AnimationInfo](../../../Murder/Core/Graphics/AnimationInfo.html) \
#### Duration
```csharp
public float Duration { get; public set; }
```

Override duration in seconds. When set to `-1` the animation's own duration is used.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
#### Loop
```csharp
public bool Loop { get; public set; }
```

Whether the animation should loop continuously. Defaults to `true`.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
#### Name
```csharp
public string Name { get; public set; }
```

The key of the animation clip to play, as defined in the sprite asset's `Animations` dictionary.

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
#### OverrideCurrentTime
```csharp
public float OverrideCurrentTime { get; public set; }
```

If different than -1, it will ignore [AnimationInfo.UseScaledTime](../../../Murder/Core/Graphics/AnimationInfo.html#usescaledtime) and use the
            time specified in this field.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
#### Start
```csharp
public float Start { get; public set; }
```

The game-time (seconds) at which playback of this animation began; used to compute the current frame offset.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
#### Ui
```csharp
public readonly static AnimationInfo Ui;
```

A ready-made `AnimationInfo` pre-configured with `UseScaledTime = true`, suitable for UI animations that respect game speed scaling.

**Returns** \
[AnimationInfo](../../../Murder/Core/Graphics/AnimationInfo.html) \
#### UseScaledTime
```csharp
public bool UseScaledTime { get; public set; }
```

When `true`, the animation uses `Game.Now` (scaled by game speed); when `false` it uses `Game.NowUnscaled`. Defaults to `false`.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \


⚡