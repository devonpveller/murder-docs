# DrawInfo

**Namespace:** Murder.Core.Graphics \
**Assembly:** Murder.dll

```csharp
public sealed struct DrawInfo
```

Generic struct for drawing things without cluttering methods full of arguments.
Note that not all fields are supported by all methods.
Tip: Create a new one like this: <code>new DrawInfo(){ Color = Color.Red, Sort = 0.2f}</code>

**Intent:** Bundles all per-draw rendering parameters (color, sort order, scale, flip, blend, outline) into a single value type so draw-call APIs stay clean.

**Use-case:** Construct a `DrawInfo` with object initializer syntax at call sites and pass it to sprite-rendering helpers like `AtlasCoordinates.Draw`, `RenderServices.DrawSprite`, or `NineSliceInfo.Draw`.

### ⭐ Constructors

```csharp
public DrawInfo()
```

```csharp
public DrawInfo(Color color, float sort)
```

**Parameters** \
`color` [Color](../../../Murder/Core/Graphics/Color.html) \
`sort` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

```csharp
public DrawInfo(float sort)
```

**Parameters** \
`sort` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

### ⭐ Properties

#### BlendMode

```csharp
public BlendStyle BlendMode { get; public set; }
```

The shader-level blend style applied to the sprite (Normal, Wash, or Color). Defaults to `BlendStyle.Normal`.

**Returns** \
[BlendStyle](../../../Murder/Core/Graphics/BlendStyle.html) \

#### BlendState

```csharp
public MurderBlendState BlendState { get; public set; }
```

The GPU blend state to use when compositing this sprite. Defaults to `MurderBlendState.AlphaBlend`; set to `MurderBlendState.Additive` for glow, light, and particle sprites that should brighten the background instead of occluding it.

**Returns** \
[MurderBlendState](../../../Murder/Core/Graphics/MurderBlendState.html) \

#### Clip

```csharp
public Rectangle Clip { get; public set; }
```

An optional source-rect clip to draw only a sub-region of the sprite. Ignored when empty.

**Returns** \
[Rectangle](../../../Murder/Core/Geometry/Rectangle.html) \

#### Color

```csharp
public Color Color { get; public set; }
```

Tint color multiplied with the sprite's texture. Defaults to `Color.White` (no tint).

**Returns** \
[Color](../../../Murder/Core/Graphics/Color.html) \

#### CultureInvariant

```csharp
public bool CultureInvariant { get; public set; }
```

Whether this draw should bypass localization fonts. Set for text/UI elements whose glyphs should render with the default font regardless of the player's selected language (e.g. debug overlays, numeric-only labels).

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### Debug

```csharp
public bool Debug { get; public set; }
```

When `true`, drawing helpers such as `RenderServices.Draw9Slice` and the pixel-font text drawers render an extra red outline (or similar diagnostic overlay) around the drawn area, to help visualize layout bounds during development.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### Default

```csharp
public static DrawInfo Default { get; }
```

A `DrawInfo` with all default values: white tint, `Sort = 0.5`, centered origin, no flip, normal blend.

**Returns** \
[DrawInfo](../../../Murder/Core/Graphics/DrawInfo.html) \

#### ImageFlip

```csharp
public ImageFlip ImageFlip { get; public set; }
```

Horizontal and/or vertical flip flags applied to the sprite. Defaults to `ImageFlip.None`.

**Returns** \
[ImageFlip](../../../Murder/Core/Graphics/ImageFlip.html) \

#### Offset

```csharp
public Vector2 Offset { get; public set; }
```

An offset to draw this image. In pixels

**Returns** \
[Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

#### Origin

```csharp
public Vector2 Origin { get; public set; }
```

The origin of the image. From 0 to 1. Vector2Helper.Center is the center.

**Returns** \
[Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

#### Outline

```csharp
public T? Outline { get; public set; }
```

Optional solid outline color drawn around the sprite according to `OutlineStyle`. `null` disables the outline.

**Returns** \
[T?](https://learn.microsoft.com/en-us/dotnet/api/System.Nullable-1?view=net-7.0) \

#### OutlineStyle

```csharp
public OutlineStyle OutlineStyle { get; public set; }
```

Flags controlling which edges of the sprite receive an outline when `Outline` is set. Defaults to `OutlineStyle.Full`.

**Returns** \
[OutlineStyle](../../../Murder/Core/Graphics/OutlineStyle.html) \

#### Rotation

```csharp
public float Rotation { get; public set; }
```

In degrees.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### Scale

```csharp
public Vector2 Scale { get; public set; }
```

Per-axis scale factor applied to the sprite. Defaults to `Vector2.One` (no scaling).

**Returns** \
[Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

#### Shadow

```csharp
public T? Shadow { get; public set; }
```

Optional drop-shadow color rendered beneath the sprite. `null` disables the shadow.

**Returns** \
[T?](https://learn.microsoft.com/en-us/dotnet/api/System.Nullable-1?view=net-7.0) \

#### Sort

```csharp
public float Sort { get; public set; }
```

Depth sort value (0 = front, 1 = back) used to order sprites within the batch when `BatchMode` is depth-sorted. Defaults to `0.5`.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

### ⭐ Methods

#### GetBlendMode()

```csharp
public Vector3 GetBlendMode()
```

Returns the `BlendMode` encoded as a `Vector3` suitable for passing to a sprite shader uniform.

**Returns** \
[Vector3](https://docs.monogame.net/api/Microsoft.Xna.Framework.Vector3.html) \

⚡
