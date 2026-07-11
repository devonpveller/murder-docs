# CameraShakeSystem

**Namespace:** Murder.Systems \
**Assembly:** Murder.dll

```csharp
public class CameraShakeSystem : IMonoPreRenderSystem, IRenderSystem, ISystem
```

Decrements the camera's shake timer each frame and clears the camera's position cache while the shake is active; resets the intensity once the timer expires.

**Intent:** Drives the camera-shake effect by consuming the shake timer and stopping the shake when it runs out.

**Use-case:** Required in any world that uses `Camera2D.ShakeTime` to produce a shake effect; no per-entity configuration is needed.

**Implements:** _[IMonoPreRenderSystem](../../Murder/Core/Graphics/IMonoPreRenderSystem.html), [IRenderSystem](../../Bang/Systems/IRenderSystem.html), [ISystem](../../Bang/Systems/ISystem.html)_

### ⭐ Constructors
```csharp
public CameraShakeSystem()
```

### ⭐ Methods
#### BeforeDraw(Context)
```csharp
public virtual void BeforeDraw(Context context)
```

Advances the camera shake timer by unscaled delta time and invalidates the camera's cached position while the shake is active.

**Parameters** \
`context` [Context](../../Bang/Contexts/Context.html) \



⚡