# RenderedSpriteReference

**Namespace:** Murder.Components.Graphics \
**Assembly:** Murder.dll

```csharp
public class RenderedSpriteReference
```

Mutable box holding the actual [RenderedSpriteCache](../../../Murder/Components/Graphics/RenderedSpriteCache.html) data for a [RenderedSpriteCacheComponent](../../../Murder/Components/Graphics/RenderedSpriteCacheComponent.html).

**Intent:** Bang components are normally immutable `readonly struct` values, replaced wholesale via `Entity.ReplaceComponent` whenever their data changes. That is too expensive to do every single frame for a per-entity render cache that changes every frame. By storing the cache data behind this ordinary (mutable, reference-type) class, `RenderServices.UpdateRenderedSpriteCache` can overwrite `Cache` in place on the existing instance shared through `RenderedSpriteCacheComponent.Ref`, refreshing the cache without allocating a new component or going through replace/equality logic.

**Use-case:** This is an internal implementation detail of `RenderedSpriteCacheComponent`; gameplay code should not construct or mutate it directly. If you need an entity's cached render state, read it through the component's proxy properties (`RenderedSpriteCacheComponent.RenderPosition`, `.CurrentAnimation`, etc.) rather than reaching into `Ref.Cache` yourself.

### ⭐ Constructors

```csharp
public RenderedSpriteReference()
```

Creates a reference wrapping a fresh, default-valued [RenderedSpriteCache](../../../Murder/Components/Graphics/RenderedSpriteCache.html).

### ⭐ Properties

#### Cache

```csharp
public RenderedSpriteCache Cache;
```

The current cached sprite render state. Overwritten in place by `RenderServices.UpdateRenderedSpriteCache` each time a render system finishes resolving an entity's draw parameters.

**Returns** \
[RenderedSpriteCache](../../../Murder/Components/Graphics/RenderedSpriteCache.html) \

⚡
