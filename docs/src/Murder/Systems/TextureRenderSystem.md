# TextureRenderSystem

**Namespace:** Murder.Systems \
**Assembly:** Murder.dll

```csharp
public class TextureRenderSystem : IMurderRenderSystem, IRenderSystem, ISystem, IReactiveSystem, IExitSystem
```

Filtered to entities with `TextureComponent`/`PositionComponent` that are not `InvisibleComponent`, and watched on `TextureComponent`. Draws the raw `Texture2D` referenced by each entity's `TextureComponent` directly to the render context, and disposes any `AutoDispose` textures when they are removed or the system exits.

**Intent:** Renders arbitrary GPU textures (not sprite-sheet animation frames, unlike the sprite-rendering systems) at an entity's world position, with support for per-entity alpha and a custom target sprite batch. It also owns the lifetime of `AutoDispose` textures, releasing their GPU resources once the entity no longer needs them.

**Use-case:** Attach `TextureComponent` to entities that hold pre-loaded `Texture2D` objects when you need direct texture rendering outside the sprite/animation system — e.g. procedurally generated textures or render targets. Set `TextureComponent.AutoDispose` to `true` if the system should own and free the underlying `Texture2D` automatically.

**Implements:** _[IMurderRenderSystem](../../Murder/Core/Graphics/IMurderRenderSystem.html), [IRenderSystem](../../Bang/Systems/IRenderSystem.html), [ISystem](../../Bang/Systems/ISystem.html), [IReactiveSystem](../../Bang/Systems/IReactiveSystem.html), [IExitSystem](../../Bang/Systems/IExitSystem.html)_

### ⭐ Constructors

```csharp
public TextureRenderSystem()
```

### ⭐ Methods

#### Draw(RenderContext, Context)

```csharp
public virtual void Draw(RenderContext render, Context context)
```

Draws each entity's `TextureComponent` texture to the specified batch at the entity's world position, applying the entity's current alpha.

**Parameters** \
`render` [RenderContext](../../Murder/Core/Graphics/RenderContext.html) \
`context` [Context](../../Bang/Contexts/Context.html) \

#### Exit(Context)

```csharp
public virtual void Exit(Context context)
```

Disposes every remaining entity's `AutoDispose` texture when the world exits, so GPU resources are not leaked when the scene is torn down.

**Parameters** \
`context` [Context](../../Bang/Contexts/Context.html) \

#### OnAdded(World, ImmutableArray<T>)

```csharp
public virtual void OnAdded(World world, ImmutableArray<T> entities)
```

No-op; nothing needs to happen when `TextureComponent` is first added, since `Draw` reads it directly every frame.

**Parameters** \
`world` [World](../../Bang/World.html) \
`entities` [ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \

#### OnModified(World, ImmutableArray<T>)

```csharp
public virtual void OnModified(World world, ImmutableArray<T> entities)
```

No-op; a modified `TextureComponent` is simply read again on the next `Draw` call.

**Parameters** \
`world` [World](../../Bang/World.html) \
`entities` [ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \

#### OnRemoved(World, ImmutableArray<T>)

```csharp
public virtual void OnRemoved(World world, ImmutableArray<T> entities)
```

Disposes the `Texture2D` of each removed entity's `TextureComponent` when `AutoDispose` is set, freeing the GPU resource as soon as the entity no longer needs it.

**Parameters** \
`world` [World](../../Bang/World.html) \
`entities` [ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \

⚡
