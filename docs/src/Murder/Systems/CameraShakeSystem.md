# CameraShakeSystem

**Namespace:** Murder.Systems \
**Assembly:** Murder.dll

```csharp
public class CameraShakeSystem : IUpdateSystem, ISystem
```

Decrements the world's `Camera2D.ShakeTime` each frame by unscaled delta time and clears the camera's position cache while the shake is active; resets the shake intensity once the timer expires.

**Intent:** Drives the camera-shake effect by consuming the shake timer and stopping the shake (and its screen-space offset) once it runs out. It is decorated with `[DoNotPause]` so the shake still winds down even while the game is paused, and `[Filter(ContextAccessorFilter.None)]` because it operates on the world's camera directly rather than on any entity.

**Use-case:** Required in any world that wants `Camera2D` shake support (typically started elsewhere by setting `camera.ShakeTime`/`ShakeIntensity`, e.g. on a hit or explosion); include it once and it will tick the timer down and invalidate the cached camera transform every frame so the shake offset is recomputed.

**Implements:** _[IUpdateSystem](../../Bang/Systems/IUpdateSystem.html), [ISystem](../../Bang/Systems/ISystem.html)_

### ⭐ Constructors

```csharp
public CameraShakeSystem()
```

### ⭐ Methods

#### Update(Context)

```csharp
public virtual void Update(Context context)
```

While `Camera2D.ShakeTime` is greater than zero, subtracts unscaled delta time from it and clears the camera's cache so the shake offset is recalculated; once the timer drops to or below zero, it is clamped to zero and `ShakeIntensity` is reset, stopping the effect.

**Parameters** \
`context` [Context](../../Bang/Contexts/Context.html) \

⚡
