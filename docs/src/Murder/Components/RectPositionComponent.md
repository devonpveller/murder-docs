# RectPositionComponent

**Namespace:** Murder.Components \
**Assembly:** Murder.dll

```csharp
public sealed struct RectPositionComponent : IParentRelativeComponent, IComponent
```

UI layout component that describes an element's box (position and size) declaratively, as padding insets and an anchor origin relative either to the screen or to a parent `RectPositionComponent`, instead of an absolute pixel position.

**Intent:** Layout a UI element using padding/anchor constraints rather than hard-coded coordinates, so it reflows automatically when the window or a parent container is resized.

**Use-case:** Attach to UI entities (panels, buttons, HUD elements) whose position should reflow with the screen or a parent container. Call `GetBox` each frame (or on layout change) to resolve the final screen-space rectangle, scaled to the current resolution via an optional reference size.

**Implements:** _[IParentRelativeComponent](../../Bang/Components/IParentRelativeComponent.html), [IComponent](../../Bang/Components/IComponent.html)_

### ⭐ Constructors

```csharp
public RectPositionComponent(float top, float left, float bottom, float right, Vector2 size, Vector2 origin, IComponent parent)
```

Creates a new UI box description from padding insets, an explicit size override, an anchor origin, and an optional parent box to lay out relative to.

**Parameters** \
`top` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`left` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`bottom` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`right` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`size` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`origin` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`parent` [IComponent](../../Bang/Components/IComponent.html) \

### ⭐ Properties

#### HasParent

```csharp
public virtual bool HasParent { get; }
```

Whether this element's box is computed relative to a parent `RectPositionComponent` rather than directly against the screen bounds.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### Origin

```csharp
public readonly Vector2 Origin;
```

Normalised anchor point within the element's box, where (0,0) is the top-left corner and (1,1) is the bottom-right corner. Used by `GetBox` to decide how the element is positioned and clipped relative to its parent/screen box once padding and size are applied.

**Returns** \
[Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

#### Size

```csharp
public readonly Vector2 Size;
```

Explicit width/height override for the element, in pixels (pre-scale). When a component is zero or negative on an axis, `GetBox` falls back to filling the parent/screen box on that axis.

**Returns** \
[Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

### ⭐ Methods

#### GetBox(Entity, Point, Point)

```csharp
public Rectangle GetBox(Entity? entity, Point screenSize, Point? referenceSize = null)
```

Resolves this element's final on-screen rectangle, walking up to the parent box (or falling back to `screenSize` if there is none), then applying padding, `Size` and `Origin`. Values are scaled by the ratio between `screenSize` and `referenceSize` so layouts designed at one resolution still look correct at another.

**Parameters** \
`entity` [Entity](../../Bang/Entities/Entity.html) \
`screenSize` [Point](../../Murder/Core/Geometry/Point.html) \
`referenceSize` [Point](../../Murder/Core/Geometry/Point.html) \

**Returns** \
[Rectangle](../../Murder/Core/Geometry/Rectangle.html) \

#### AddPadding(RectPositionComponent)

```csharp
public RectPositionComponent AddPadding(RectPositionComponent b)
```

Returns a copy of this component with each padding value increased by the corresponding padding value of `b`. Useful for compositing an extra inset (e.g. a nested panel's own margin) on top of an existing layout without recomputing every field by hand.

**Parameters** \
`b` [RectPositionComponent](../../Murder/Components/RectPositionComponent.html) \

**Returns** \
[RectPositionComponent](../../Murder/Components/RectPositionComponent.html) \

#### WithSize(Vector2)

```csharp
public RectPositionComponent WithSize(Vector2 size)
```

Returns a copy of this component with `Size` replaced by the given value, keeping all padding, origin and parent settings unchanged.

**Parameters** \
`size` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

**Returns** \
[RectPositionComponent](../../Murder/Components/RectPositionComponent.html) \

#### WithoutParent()

```csharp
public virtual IParentRelativeComponent WithoutParent()
```

Returns a copy of this component with its parent reference cleared, so the resulting box is laid out directly against the screen bounds instead of a parent element's box.

**Returns** \
[IParentRelativeComponent](../../Bang/Components/IParentRelativeComponent.html) \

#### OnParentModified(IComponent, Entity)

```csharp
public virtual void OnParentModified(IComponent parentComponent, Entity childEntity)
```

Called by the engine when this entity's parent's `RectPositionComponent` changes, so this element's cached parent box is kept in sync and `GetBox` resolves against the parent's latest layout.

**Parameters** \
`parentComponent` [IComponent](../../Bang/Components/IComponent.html) \
`childEntity` [Entity](../../Bang/Entities/Entity.html) \

⚡
