# CameraServices

**Namespace:** Murder.Services \
**Assembly:** Murder.dll

```csharp
public static class CameraServices
```

Provides utility methods for controlling the game camera: retargeting what it follows and applying kinetic feedback (shake and bump).

**Intent:** Wraps the low-level [CameraFollowComponent](../../Murder/Components/CameraFollowComponent.html) manipulation and `MonoWorld.Camera` state behind a small, intention-revealing API so gameplay code does not need to know how camera targeting or shake accumulation is implemented internally.

**Use-case:** Call `AddSecondaryTarget`/`RemoveSecondaryTarget` when a cutscene or scripted event needs the camera to temporarily track something other than (or in addition to) the player. Call `ShakeCamera` for impact feedback (explosions, hits, screen-rumble) and `BumpCamera` for a short directional/one-off punch of camera movement — both are common calls from `IInteractiveComponent`/`IMessager` implementations and combat/feedback systems reacting to gameplay events.

### ⭐ Methods

#### AddSecondaryTarget(World, Entity)

```csharp
public static void AddSecondaryTarget(World world, Entity secondaryTarget)
```

Points the world's unique camera-follow entity at `secondaryTarget` in addition to its normal target, replacing the existing `CameraFollowComponent` with one that has `SecondaryTarget` enabled and clearing any active ID target. Use this to have the camera track a boss, a cutscene focal point, or another entity of interest without losing track of the primary target semantics — for example, widening the framing so both the player and an important object stay on screen.

**Parameters** \
`world` [World](../../Bang/World.html) \
`secondaryTarget` [Entity](../../Bang/Entities/Entity.html) \

#### RemoveSecondaryTarget(World)

```csharp
public static void RemoveSecondaryTarget(World world)
```

Resets the world's unique camera-follow entity back to a single-target `CameraFollowComponent`, clearing any secondary target and ID target that were previously set. Call this to restore normal camera-follow behavior once a scripted sequence that used `AddSecondaryTarget` has finished.

**Parameters** \
`world` [World](../../Bang/World.html) \

#### ShakeCamera(World, float, float)

```csharp
public static void ShakeCamera(World world, float intensity, float time)
```

Applies a screen-shake effect to the world's `MonoWorld.Camera`. If a shake is already in progress with a *lower* intensity than `intensity`, the two are blended via `Calculator.Lerp` instead of being replaced outright, and the shake duration is extended to whichever of the current or the new `time` is longer. This means repeated calls (e.g. from a burst of hits) accumulate smoothly rather than resetting or fighting each other — the typical use is calling this once per impactful gameplay event (hit received, explosion, heavy landing) and letting the camera system handle blending.

**Parameters** \
`world` [World](../../Bang/World.html) \
`intensity` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`time` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### BumpCamera(World, float)

```csharp
public static void BumpCamera(World world, float intensity)
```

Casts `world` to `MonoWorld` and calls `Camera.Bump(intensity)`, giving the camera a short, single directional kick rather than a sustained random shake. Use this for punchier, more directional feedback (e.g. a single hard hit or a jump landing) where a full shake would feel too noisy.

**Parameters** \
`world` [World](../../Bang/World.html) \
`intensity` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

⚡
