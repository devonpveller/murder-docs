# SharedResources

**Namespace:** Murder.Core.Graphics \
**Assembly:** Murder.dll

```csharp
public static class SharedResources
```

Shared resources used per game instance.
            TODO: Move to RenderContext?

**Intent:** Provides lazily created, shared GPU resources (e.g. a 1×1 white pixel texture) that are expensive to recreate and safe to reuse across all render contexts.

**Use-case:** Call `GetOrCreatePixel()` whenever you need a small blank texture for drawing solid-color shapes without allocating a new `Texture2D` each time.

### ⭐ Methods
#### CreatePixel(Color)
```csharp
public Texture2D CreatePixel(Color color)
```

Creates a new 1x1 pixel texture with a given color

**Parameters** \
`color` [Color](../../../Murder/Core/Graphics/Color.html) \
\

**Returns** \
[Texture2D](https://docs.monogame.net/api/Microsoft.Xna.Framework.Graphics.Texture2D.html) \
\

#### GetOrCreatePixel()
```csharp
public Texture2D GetOrCreatePixel()
```

Returns the shared 1×1 white pixel texture, creating it if it does not yet exist.

**Returns** \
[Texture2D](https://docs.monogame.net/api/Microsoft.Xna.Framework.Graphics.Texture2D.html) \



⚡