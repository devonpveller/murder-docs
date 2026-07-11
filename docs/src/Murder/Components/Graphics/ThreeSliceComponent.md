# ThreeSliceComponent

**Namespace:** Murder.Components.Graphics \
**Assembly:** Murder.dll

```csharp
public sealed struct ThreeSliceComponent : IComponent
```

This component makes sure that any aseprite will render as a 3-slice instead,
            as specified.

**Intent:** Render a sprite using 3-slice scaling so the ends are drawn at their original size while only the middle section is stretched.

**Use-case:** Add to UI elements or environmental props (such as platforms or panels) that need to scale along one axis without distorting the end caps.

**Implements:** _[IComponent](../../../Bang/Components/IComponent.html)_

### ⭐ Constructors
```csharp
public ThreeSliceComponent()
```

### ⭐ Properties
#### CoreSliceRectangle
```csharp
public readonly Rectangle CoreSliceRectangle;
```

The rectangle within the source sprite that defines the stretchable center slice.

**Returns** \
[Rectangle](../../../Murder/Core/Geometry/Rectangle.html) \
#### Orientation
```csharp
public readonly Orientation Orientation;
```

Axis along which the sprite is sliced and stretched (horizontal or vertical).

**Returns** \
[Orientation](../../../Murder/Core/Orientation.html) \
#### Size
```csharp
public readonly int Size;
```

Target length (in pixels) of the full rendered sprite along the slice axis.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \


⚡