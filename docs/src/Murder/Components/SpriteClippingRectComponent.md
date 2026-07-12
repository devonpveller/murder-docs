# SpriteClippingRectComponent

**Namespace:** Murder.Components \
**Assembly:** Murder.dll

```csharp
public sealed struct SpriteClippingRectComponent : IComponent
```

Defines a clipping rectangle that masks a portion of the entity's sprite, allowing it to grow or shrink from the center or be cut from its borders.

**Intent:** Dynamically reveal or hide parts of a sprite using a rectangular mask, without needing a separate render target or shader.

**Use-case:** Attach to an entity with a `SpriteComponent`; `SpriteRenderSystem` checks for it (`e.TryGetSpriteClippingRect()`) and, when present, calls `GetClippingRect(asset.Size, asset.Origin)` to compute the visible sub-rectangle of the sprite's frame, using it both to source-clip the draw call and to offset the render position by the clip's top-left. Useful for a health bar or progress fill that grows/shrinks (`GrowFromCenter`), or a UI element that slides in/out from one edge (`CutFromBorders`).

**Implements:** _[IComponent](../../Bang/Components/IComponent.html)_

### ⭐ Constructors

```csharp
public SpriteClippingRectComponent(float left, float right, float top, float down, ClippingStyle clippingStyle)
```

**Parameters** \
`left` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`right` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`top` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`down` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`clippingStyle` [ClippingStyle](../../Murder/Components/ClippingStyle.html) \

### ⭐ Properties

#### Down

```csharp
public readonly float Down;
```

Clipping amount on the bottom edge (0 = no clip, 1 = fully clipped from that edge).

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### Left

```csharp
public readonly float Left;
```

Clipping amount on the left edge.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### Right

```csharp
public readonly float Right;
```

Clipping amount on the right edge.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### Style

```csharp
public readonly ClippingStyle Style;
```

Determines whether the clip grows from the center outward or cuts from the borders inward.

**Returns** \
[ClippingStyle](../../Murder/Components/ClippingStyle.html) \

#### Top

```csharp
public readonly float Top;
```

Clipping amount on the top edge.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

### ⭐ Methods

#### GetClippingRect(Point, Point)

```csharp
public Rectangle GetClippingRect(Point spriteSize, Point origin)
```

Calculates the source clipping rectangle in sprite-pixel space for the current `Left`, `Right`, `Top`, and `Down` values. When `Style` is `GrowFromCenter`, `origin` is used as the center the rectangle expands outward from (a value of `-1` on any side means "extend fully to that edge"); when `Style` is `CutFromBorders`, `origin` is ignored and the rectangle is simply inset from each border by the corresponding amount. Throws `ArgumentOutOfRangeException` if `Style` holds a value outside the `ClippingStyle` enum.

**Parameters** \
`spriteSize` [Point](../../Murder/Core/Geometry/Point.html) \
`origin` [Point](../../Murder/Core/Geometry/Point.html) \

**Returns** \
[Rectangle](../../Murder/Core/Geometry/Rectangle.html) \

**Exceptions** \
[ArgumentOutOfRangeException](https://learn.microsoft.com/en-us/dotnet/api/System.ArgumentOutOfRangeException?view=net-7.0) \

⚡
