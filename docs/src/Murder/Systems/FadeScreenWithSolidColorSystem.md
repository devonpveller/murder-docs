# FadeScreenWithSolidColorSystem

**Namespace:** Murder.Systems \
**Assembly:** Murder.dll

```csharp
public class FadeScreenWithSolidColorSystem : IReactiveSystem, IMurderRenderSystem, IRenderSystem, IExitSystem, ISystem
```

System responsible for fading in and out entities.
This is not responsible for the screen fade transition.

**Intent:** Renders a full-screen solid-color overlay that fades in or out, enabling smooth screen-wipe transitions between scenes or states. Unlike `FadeTransitionSystem`, this is a raw solid-color fade with no gradient asset — it exists for simple black/white screen fades where a texture-based transition isn't needed.

**Use-case:** Add a `FadeScreenWithSolidColorComponent` to a world entity (with `FadeType.In` or `FadeType.Out`) when you need a screen fade (e.g., fade to black before loading a new scene); this system reads the component reactively, drives the alpha interpolation inside `Draw`, and paints the overlay rectangle over the target sprite batch each frame. It is decorated with `[DoNotPause]` so a fade-to-black around a pause menu still plays out.

**Implements:** _[IReactiveSystem](../../Bang/Systems/IReactiveSystem.html), [IMurderRenderSystem](../../Murder/Core/Graphics/IMurderRenderSystem.html), [IRenderSystem](../../Bang/Systems/IRenderSystem.html), [IExitSystem](../../Bang/Systems/IExitSystem.html), [ISystem](../../Bang/Systems/ISystem.html)_

### ⭐ Constructors

```csharp
public FadeScreenWithSolidColorSystem()
```

### ⭐ Methods

#### OnAdded(World, ImmutableArray<T>)

```csharp
public virtual void OnAdded(World world, ImmutableArray<T> entities)
```

Delegates to `OnModified` to configure the fade parameters from the newly added `FadeScreenWithSolidColorComponent`.

**Parameters** \
`world` [World](../../Bang/World.html) \
`entities` [ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \

#### OnModified(World, ImmutableArray<T>)

```csharp
public virtual void OnModified(World world, ImmutableArray<T> entities)
```

Reads the `FadeScreenWithSolidColorComponent` from the (single expected) modified entity and updates internal fade-in/fade-out timers, color, duration, sort order, and target sprite batch. If more than one entity carries the component in the same frame it logs a warning and prefers the one requesting `FadeType.Out`.

**Parameters** \
`world` [World](../../Bang/World.html) \
`entities` [ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \

#### OnRemoved(World, ImmutableArray<T>)

```csharp
public virtual void OnRemoved(World world, ImmutableArray<T> entities)
```

No-op; the fade component is typically left in place (or removed by the caller) once it has finished, and no per-entity state needs cleanup here.

**Parameters** \
`world` [World](../../Bang/World.html) \
`entities` [ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \

#### Draw(RenderContext, Context)

```csharp
public virtual void Draw(RenderContext render, Context context)
```

Advances the fade-in/fade-out alpha interpolation based on elapsed unscaled time, then draws a solid-color rectangle covering the camera's safe bounds (or the UI-relative area, depending on target batch) onto the configured sprite batch at the configured sort order. Also mirrors the resulting alpha onto `RenderContext.ScreenFade` and invokes `OnAlphaUpdateImpl` whenever the rounded alpha changes, so a fully transparent fade draws nothing at all.

**Parameters** \
`render` [RenderContext](../../Murder/Core/Graphics/RenderContext.html) \
`context` [Context](../../Bang/Contexts/Context.html) \

#### OnAlphaUpdateImpl(float)

```csharp
protected virtual void OnAlphaUpdateImpl(float alpha)
```

Empty extension hook invoked once per frame whenever the fade's rounded alpha value changes. Override it in a derived system to react to fade progress (e.g. triggering an event exactly when the screen is fully black).

**Parameters** \
`alpha` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### Exit(Context)

```csharp
public virtual void Exit(Context context)
```

Resets the active scene's `RenderContext.ScreenFade` back to zero when the world exits, so a lingering fade value doesn't bleed into whatever renders next.

**Parameters** \
`context` [Context](../../Bang/Contexts/Context.html) \

⚡
