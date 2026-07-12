# PolygonSpriteComponent

**Namespace:** Murder.Components \
**Assembly:** Murder.dll

```csharp
public sealed struct PolygonSpriteComponent : IComponent
```

Renders one or more filled polygons as a sprite-like visual on an entity. Each shape in the list is drawn using the specified color and sorted by the `SortOffset` value.

**Intent:** Draw procedural polygon geometry directly on an entity without requiring a texture or atlas asset.

**Use-case:** Use for debug overlays, simple geometric entities, or UI elements that need solid-color polygon shapes rendered in the game world.

**Implements:** _[IComponent](../../Bang/Components/IComponent.html)_

### ⭐ Constructors

```csharp
public PolygonSpriteComponent()
```

### ⭐ Properties

#### Batch

```csharp
public readonly int Batch;
```

Sprite batch layer used when rendering these polygons.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### Color

```csharp
public readonly Color Color;
```

Fill color applied to all shapes in the collection.

**Returns** \
[Color](../../Murder/Core/Graphics/Color.html) \

#### Shapes

```csharp
public readonly ImmutableArray<T> Shapes;
```

The polygon shapes to be drawn on the entity.

**Returns** \
[ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \

#### SortOffset

```csharp
public readonly int SortOffset;
```

Vertical sort offset applied when determining draw order relative to other entities.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

⚡
