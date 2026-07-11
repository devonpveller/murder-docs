# FadeScreenWithSolidColorSystem

**Namespace:** Murder.Systems \
**Assembly:** Murder.dll

```csharp
public class FadeScreenWithSolidColorSystem : IUpdateSystem, ISystem, IReactiveSystem, IMurderRenderSystem, IRenderSystem
```

System responsible for fading in and out entities.
            This is not responsible for the screen fade transition.

**Intent:** Renders a full-screen solid-color overlay that fades in or out, enabling smooth screen-wipe transitions between scenes or states.

**Use-case:** Add a `FadeScreenWithSolidColorComponent` to a world entity when you need a screen fade (e.g., fade to black before loading a new scene); this system drives the interpolation and draws the overlay.

**Implements:** _[IUpdateSystem](../../Bang/Systems/IUpdateSystem.html), [ISystem](../../Bang/Systems/ISystem.html), [IReactiveSystem](../../Bang/Systems/IReactiveSystem.html), [IMurderRenderSystem](../../Murder/Core/Graphics/IMurderRenderSystem.html), [IRenderSystem](../../Bang/Systems/IRenderSystem.html)_

### ⭐ Constructors
```csharp
public FadeScreenWithSolidColorSystem()
```

### ⭐ Methods
#### Draw(RenderContext, Context)
```csharp
public virtual void Draw(RenderContext render, Context context)
```

**Parameters** \
`render` [RenderContext](../../Murder/Core/Graphics/RenderContext.html) \
`context` [Context](../../Bang/Contexts/Context.html) \

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

Reads the `FadeScreenWithSolidColorComponent` from the modified entity and updates internal fade-in/fade-out timers, color, duration, sort order, and target batch.

**Parameters** \
`world` [World](../../Bang/World.html) \
`entities` [ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \

#### OnRemoved(World, ImmutableArray<T>)
```csharp
public virtual void OnRemoved(World world, ImmutableArray<T> entities)
```

No-op; cleanup when the component is removed is handled elsewhere.

**Parameters** \
`world` [World](../../Bang/World.html) \
`entities` [ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \

#### Update(Context)
```csharp
public virtual void Update(Context context)
```

Advances the alpha interpolation each frame based on elapsed time; does nothing if no fade is currently active.

**Parameters** \
`context` [Context](../../Bang/Contexts/Context.html) \



⚡