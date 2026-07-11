# NineSliceComponent

**Namespace:** Murder.Components \
**Assembly:** Murder.dll

```csharp
public sealed struct NineSliceComponent : IComponent
```

This component makes sure that any sprite will render as a 9-slice instead,
            as specified.

**Intent:** Render a sprite asset as a 9-slice so that it scales to an arbitrary size without distorting the corners or edges.

**Use-case:** Add to UI panels, dialogue boxes, or scalable world objects and set `Target` to the desired output rectangle; the renderer stretches only the center regions while keeping corners and edges pixel-perfect.

**Implements:** _[IComponent](../../Bang/Components/IComponent.html)_

### ⭐ Constructors
```csharp
public NineSliceComponent()
```

### ⭐ Properties
#### Sprite
```csharp
public readonly Guid Sprite;
```

GUID of the sprite asset to draw as a 9-slice.

**Returns** \
[Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \
#### Style
```csharp
public readonly NineSliceStyle Style;
```

Determines how the center region of the nine-slice is scaled (e.g. stretch or tile).

**Returns** \
[NineSliceStyle](../../Murder/Core/Graphics/NineSliceStyle.html) \
#### Target
```csharp
public readonly Rectangle Target;
```

Destination rectangle defining the final rendered size and position of the nine-slice sprite.

**Returns** \
[Rectangle](../../Murder/Core/Geometry/Rectangle.html) \
#### TargetSpriteBatch
```csharp
public readonly int TargetSpriteBatch;
```

ID of the sprite batch layer on which this nine-slice is drawn.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
#### YSortOffset
```csharp
public readonly int YSortOffset;
```

Pixel offset added to the entity's Y position when computing the draw-order sort key.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \


⚡