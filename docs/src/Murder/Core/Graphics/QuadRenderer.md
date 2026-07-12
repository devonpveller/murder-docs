# QuadRenderer

**Namespace:** Murder.Core.Graphics \
**Assembly:** Murder.dll

```csharp
public class QuadRenderer
```

Renders a simple quad to the screen. Uncomment the Vertex / Index buffers to make it a static fullscreen quad.
The performance effect is barely measurable though and you need to dispose of the buffers when finished!

**Intent:** Provides a minimal GPU path for drawing a single screen-space quad, typically used as a full-screen blit for post-processing passes.

**Use-case:** Instantiate once per render context and call `RenderQuad()` each frame to push a shader-driven quad through the GPU without the overhead of a sprite batch. Nothing in the base Murder engine currently instantiates `QuadRenderer` — the engine's actual full-screen blits go through `RenderServices.DrawTextureQuad`/`Batch2D` — so treat this as a low-level utility available for a game's own custom `RenderContext` post-processing passes rather than something wired into the default pipeline.

### ⭐ Constructors

```csharp
public QuadRenderer(GraphicsDevice _)
```

Initializes the vertex and index buffers for a screen-space quad. The `GraphicsDevice` parameter is accepted for API compatibility but not stored.

**Parameters** \
`_` [GraphicsDevice](https://docs.monogame.net/api/Microsoft.Xna.Framework.Graphics.GraphicsDevice.html) \

### ⭐ Methods

#### RenderQuad(GraphicsDevice, Vector2, Vector2)

```csharp
public void RenderQuad(GraphicsDevice graphicsDevice, Vector2 v1, Vector2 v2)
```

Draws a single quad from corner `v1` to corner `v2` using the provided graphics device and the current shader state.

**Parameters** \
`graphicsDevice` [GraphicsDevice](https://docs.monogame.net/api/Microsoft.Xna.Framework.Graphics.GraphicsDevice.html) \
`v1` [Vector2](https://docs.monogame.net/api/Microsoft.Xna.Framework.Vector2.html) \
`v2` [Vector2](https://docs.monogame.net/api/Microsoft.Xna.Framework.Vector2.html) \

⚡
