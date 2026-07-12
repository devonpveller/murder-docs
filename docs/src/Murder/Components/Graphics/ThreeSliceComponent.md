# ThreeSliceComponent

**Namespace:** Murder.Components.Graphics \
**Assembly:** Murder.dll

```csharp
public sealed struct ThreeSliceComponent : IComponent
```

This component makes sure that any aseprite will render as a 3-slice instead,
as specified.

**Intent:** Render a sprite using 3-slice scaling — the two end caps are drawn at their original size while only the middle section is stretched to fill `Size` — instead of the sprite's normal 1:1 draw. `SpriteThreeSliceRenderSystem` is the dedicated render system for this: it filters for entities that have both this component and a `PositionComponent`, reads the entity's `SpriteComponent` to resolve the source frame, and calls `RenderServices.Draw3Slice` with `CoreSliceRectangle`, `Size`, and `Orientation`. Because this is a distinct render path, `SpriteRenderSystem` explicitly excludes any entity that has a `ThreeSliceComponent` (`[Filter(ContextAccessorFilter.NoneOf, typeof(ThreeSliceComponent), ...)]`) so the two systems never both draw the same sprite.

**Use-case:** Add to UI elements or environmental props (such as platforms, bars, or panels) that need to scale along one axis without distorting the end caps. The component is decorated with `[Requires(typeof(SpriteComponent))]`, so an entity must already have (or receive alongside it) a `SpriteComponent` supplying the source aseprite/atlas frame — `ThreeSliceComponent` only carries the slicing parameters, not the sprite reference itself.

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
