# DrawRectangleComponent

**Namespace:** Murder.Components \
**Assembly:** Murder.dll

```csharp
public sealed struct DrawRectangleComponent : IComponent
```

Renders a filled or outlined rectangle at the entity's position each frame.

**Implements:** _[IComponent](../../Bang/Components/IComponent.html)_

**Intent:** Provides a simple primitive drawing capability for entities that need a solid or outlined rectangle without a full sprite asset. `RectangleRenderSystem` draws it every frame at the entity's global position, using the entity's [ColliderComponent](../../Murder/Components/ColliderComponent.html) bounding box when present (falling back to a single grid cell otherwise) and respecting any [AlphaComponent](../../Murder/Components/AlphaComponent.html) alpha.

**Use-case:** Attach to debug overlays, UI elements, or simple gameplay shapes such as selection boxes or area indicators; configure `Color`, `Fill`, and `TargetSpriteBatch` as needed. When `Fill` is `true`, set `SmoothSize`/`SmoothingLayers` to draw progressively larger, more transparent copies of the rectangle underneath it for a soft glow/blur edge instead of a hard-edged fill.

### ⭐ Constructors

```csharp
public DrawRectangleComponent()
```

```csharp
public DrawRectangleComponent(int spriteBatch, bool fill, Color color, float offset)
```

**Parameters** \
`spriteBatch` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`fill` [bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
`color` [Color](../../Murder/Core/Graphics/Color.html) \
`offset` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

### ⭐ Properties

#### Color

```csharp
public readonly Color Color;
```

Color of the rectangle (fill color or outline color depending on `Fill`).

**Returns** \
[Color](../../Murder/Core/Graphics/Color.html) \

#### Fill

```csharp
public readonly bool Fill;
```

When `true`, the rectangle is drawn filled; when `false`, only the outline is drawn.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### LineWidth

```csharp
public readonly int LineWidth;
```

Width in pixels of the outline when `Fill` is `false`.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### SmoothingLayers

```csharp
public readonly int SmoothingLayers;
```

Number of extra faded copies of the rectangle drawn underneath the fill, each progressively larger (up to `SmoothSize`) and more transparent. Only applies when `Fill` is `true`; `0` (the default) draws a plain hard-edged fill.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### SmoothSize

```csharp
public readonly float SmoothSize;
```

Maximum pixel expansion used for the outermost smoothing layer when `SmoothingLayers` is greater than zero, producing a soft glow-like edge around the filled rectangle.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### SortingOffset

```csharp
public readonly float SortingOffset;
```

Vertical pixel offset added to Y when computing draw-order sorting.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### TargetSpriteBatch

```csharp
public readonly int TargetSpriteBatch;
```

Index of the sprite batch that this rectangle is submitted to during rendering.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

⚡
