# TextureRenderSystem

**Namespace:** Murder.Systems \
**Assembly:** Murder.dll

```csharp
public class TextureRenderSystem : IMurderRenderSystem, IRenderSystem, ISystem, IReactiveSystem, IExitSystem
```

Draws raw `Texture2D` resources from `TextureComponent` entities to the render context and optionally disposes auto-dispose textures when the system exits.

**Intent:** Renders arbitrary GPU textures (not sprite-sheet frames) at an entity's world position with support for per-entity alpha and custom batch targets.

**Use-case:** Attach `TextureComponent` to entities that hold pre-loaded `Texture2D` objects when you need direct texture rendering outside the sprite system.

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
Disposals textures marked with `AutoDispose` when the world exits to free GPU resources.
**Parameters** \
`context` [Context](../../Bang/Contexts/Context.html) \

```csharp
public virtual void OnAdded(World world, ImmutableArray<T> entities)
```

Called when `TextureComponent` is added to entities; reserved for subclass extension.

**Parameters** \
`world` [World](../../Bang/World.html) \
`entities` [ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \

```csharp
public virtual void OnModified(World world, ImmutableArray<T> entities)
```

Called when `TextureComponent` is modified on entities; reserved for subclass extension.

**Parameters** \
`world` [World](../../Bang/World.html) \
`entities` [ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \

```csharp
public virtual void OnRemoved(World world, ImmutableArray<T> entities)
```

Called when `TextureComponent` is removed from entities; reserved for subclass extension.

**Parameters** \
`world` [World](../../Bang/World.html) \
`entities` [ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \



⚡