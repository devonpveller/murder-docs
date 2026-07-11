# DrawRectangleComponent

**Namespace:** Murder.Components \
**Assembly:** Murder.dll

```csharp
public sealed struct DrawRectangleComponent : IComponent
```

Renders a filled or outlined rectangle at the entity's position each frame.

**Implements:** _[IComponent](../../Bang/Components/IComponent.html)_

**Intent:** Provides a simple primitive drawing capability for entities that need a solid or outlined rectangle without a full sprite asset.

**Use-case:** Attach to debug overlays, UI elements, or simple gameplay shapes such as selection boxes or area indicators; configure `Color`, `Fill`, and `TargetSpriteBatch` as needed.

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