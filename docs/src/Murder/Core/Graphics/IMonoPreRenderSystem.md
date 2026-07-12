# IMonoPreRenderSystem

**Namespace:** Murder.Core.Graphics \
**Assembly:** Murder.dll

```csharp
public abstract IMonoPreRenderSystem : IRenderSystem, ISystem
```

System called right before rendering.

**Intent:** Marks an ECS system as a pre-render hook that runs once per frame, before `RenderContext.Begin()` (and therefore before any `Batch2D.Begin()` call), so it can compute or update render-affecting component state that the actual draw-pass systems (`IMurderRenderSystem`) will read.

**Use-case:** The dominant real-world use is precomputing transient, per-entity values that influence how something is drawn this frame — fade alpha (`FadeSpriteSystem`), which animation frame is active (`SpriteAnimationStarterSystem`), a squish/scale factor (`SquishSystem`), or camera-visibility flags used for culling (`DynamicInCameraSystem`, `StaticInCameraSystem`). Because it runs before GPU state is touched, it can also be used to prepare render targets or shared shader parameters, but in practice the engine's own `IMonoPreRenderSystem` implementations are all "compute a component value" systems rather than GPU-state systems. `MonoWorld.PreDraw()` calls `BeforeDraw` on every active system of this kind, once per frame, before `World.Draw`.

**Implements:** _[IRenderSystem](../../../Bang/Systems/IRenderSystem.html), [ISystem](../../../Bang/Systems/ISystem.html)_

### ⭐ Methods

#### BeforeDraw(Context)

```csharp
public abstract void BeforeDraw(Context context)
```

Called once per frame, before rendering starts — specifically before `RenderContext.Begin()`/`Batch2D.Begin()` and `Batch2D.End()`. Use it to write to components that the subsequent `IMurderRenderSystem.Draw` pass will read, not to issue draw calls directly.

**Parameters** \
`context` [Context](../../../Bang/Contexts/Context.html) \

⚡
