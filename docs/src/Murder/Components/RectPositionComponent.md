# RectPositionComponent

**Namespace:** Murder.Components \
**Assembly:** Murder.dll

```csharp
public sealed struct RectPositionComponent : IParentRelativeComponent, IComponent
```

UI position component that calculates an entity's on-screen rectangle from padding and size values relative to its parent or the screen bounds.

**Intent:** Layout a UI element using CSS-like padding constraints rather than absolute coordinates.

**Use-case:** Attach to UI entities whose position should reflow automatically when the parent container or screen size changes.

**Implements:** _[IParentRelativeComponent](../../Bang/Components/IParentRelativeComponent.html), [IComponent](../../Bang/Components/IComponent.html)_

### ⭐ Constructors
```csharp
public RectPositionComponent(float top, float left, float bottom, float right, Vector2 size, Vector2 origin, IComponent parent)
```

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

Whether this component is positioned relative to a parent component.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
#### Origin
```csharp
public readonly Vector2 Origin;
```

Normalised anchor point within the element where (0,0) is top-left and (1,1) is bottom-right.

**Returns** \
[Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
#### Size
```csharp
public readonly Vector2 Size;
```

Explicit size override for the element. Used when the size cannot be inferred from the content.

**Returns** \
[Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
### ⭐ Methods
#### GetBox(Entity, Point, T?)
```csharp
public Rectangle GetBox(Entity entity, Point screenSize, T? referenceSize)
```

Calculates the screen-space rectangle for this element given the entity, current screen size, and an optional reference size.

**Parameters** \
`entity` [Entity](../../Bang/Entities/Entity.html) \
`screenSize` [Point](../../Murder/Core/Geometry/Point.html) \
`referenceSize` [T?](https://learn.microsoft.com/en-us/dotnet/api/System.Nullable-1?view=net-7.0) \

**Returns** \
[Rectangle](../../Murder/Core/Geometry/Rectangle.html) \

#### AddPadding(RectPositionComponent)
```csharp
public RectPositionComponent AddPadding(RectPositionComponent b)
```

Returns a new component with the padding values of `b` added to this component's padding.

**Parameters** \
`b` [RectPositionComponent](../../Murder/Components/RectPositionComponent.html) \

**Returns** \
[RectPositionComponent](../../Murder/Components/RectPositionComponent.html) \

#### WithSize(Vector2)
```csharp
public RectPositionComponent WithSize(Vector2 size)
```

Returns a new component with the `Size` field replaced by the given value.

**Parameters** \
`size` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

**Returns** \
[RectPositionComponent](../../Murder/Components/RectPositionComponent.html) \

#### WithoutParent()
```csharp
public virtual IParentRelativeComponent WithoutParent()
```

Returns a copy of this component with the parent reference removed.

**Returns** \
[IParentRelativeComponent](../../Bang/Components/IParentRelativeComponent.html) \

#### OnParentModified(IComponent, Entity)
```csharp
public virtual void OnParentModified(IComponent parentComponent, Entity childEntity)
```

Called by the engine when the parent component changes; updates this element's position to match the new parent bounds.

**Parameters** \
`parentComponent` [IComponent](../../Bang/Components/IComponent.html) \
`childEntity` [Entity](../../Bang/Entities/Entity.html) \



⚡