# SpriteClippingRectComponent

**Namespace:** Murder.Components \
**Assembly:** Murder.dll

```csharp
public sealed struct SpriteClippingRectComponent : IComponent
```

Defines a clipping rectangle that masks a portion of the entity's sprite, allowing it to grow or shrink from the center or be cut from its borders.

**Intent:** Dynamically reveal or hide parts of a sprite using a rectangular mask.

**Use-case:** Attach to a health-bar sprite to animate it filling or draining, or to a UI element that should slide in from one edge.

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
#### GetClippingRect(Point)
```csharp
public Rectangle GetClippingRect(Point spriteSize)
```

Calculates the source clipping rectangle in sprite-pixel space for the current `Left`, `Right`, `Top`, and `Down` values.

**Parameters** \
`spriteSize` [Point](../../Murder/Core/Geometry/Point.html) \

**Returns** \
[Rectangle](../../Murder/Core/Geometry/Rectangle.html) \



⚡