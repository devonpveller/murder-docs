# VertexInfo

**Namespace:** Murder.Core.Graphics \
**Assembly:** Murder.dll

```csharp
public sealed struct VertexInfo : IVertexType
```

A single GPU vertex holding world-space position, tint color, atlas UV, and a blend-mode selector.

**Intent:** Represents the raw vertex data passed to the GPU for each corner of a sprite quad, carrying all information the sprite shader needs to sample and tint the texture.

**Use-case:** Populated automatically by `SpriteBatchItem.Set()`; inspect or modify `VertexData` directly for custom geometry in `SpriteBatchItem.SetPolygon()`.

**Implements:** _[IVertexType](https://docs.monogame.net/api/Microsoft.Xna.Framework.Graphics.IVertexType.html)_

### ⭐ Constructors
```csharp
public VertexInfo(Vector3 position, Color color, Vector2 textureCoord, Vector3 blend)
```

Creates a vertex with explicit position (XY + depth), tint color, atlas UV, and blend selector.

**Parameters** \
`position` [Vector3](https://docs.monogame.net/api/Microsoft.Xna.Framework.Vector3.html) \
`color` [Color](https://docs.monogame.net/api/Microsoft.Xna.Framework.Color.html) \
`textureCoord` [Vector2](https://docs.monogame.net/api/Microsoft.Xna.Framework.Vector2.html) \
`blend` [Vector3](https://docs.monogame.net/api/Microsoft.Xna.Framework.Vector3.html) \

### ⭐ Properties
#### BlendType
```csharp
public Vector3 BlendType;
```

A `Vector3` selector passed to the sprite shader to choose between normal alpha blend, color wash, and solid-color blend modes.

**Returns** \
[Vector3](https://docs.monogame.net/api/Microsoft.Xna.Framework.Vector3.html) \
#### Color
```csharp
public Color Color;
```

Tint color multiplied with the texture sample by the GPU shader.

**Returns** \
[Color](https://docs.monogame.net/api/Microsoft.Xna.Framework.Color.html) \
#### Position
```csharp
public Vector3 Position;
```

World-space position of this vertex; the Z component carries the depth/sort value for the renderer.

**Returns** \
[Vector3](https://docs.monogame.net/api/Microsoft.Xna.Framework.Vector3.html) \
#### TextureCoordinate
```csharp
public Vector2 TextureCoordinate;
```

Normalized UV coordinate into the atlas texture sampled at this vertex.

**Returns** \
[Vector2](https://docs.monogame.net/api/Microsoft.Xna.Framework.Vector2.html) \
#### VertexDeclaration
```csharp
public readonly static VertexDeclaration VertexDeclaration;
```

Shared `VertexDeclaration` describing the memory layout (position, color, UV, blend) for the GPU input assembler.

**Returns** \
[VertexDeclaration](https://docs.monogame.net/api/Microsoft.Xna.Framework.Graphics.VertexDeclaration.html) \
### ⭐ Methods
#### Equals(Object)
```csharp
public virtual bool Equals(Object obj)
```

**Parameters** \
`obj` [Object](https://learn.microsoft.com/en-us/dotnet/api/System.Object?view=net-7.0) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### GetHashCode()
```csharp
public virtual int GetHashCode()
```

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### ToString()
```csharp
public virtual string ToString()
```

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \



⚡