# NodeInfo\<T\>

**Namespace:** Murder.Core.Physics \
**Assembly:** Murder.dll

```csharp
public sealed struct NodeInfo<T>
```

Pairs an entity payload `T` with its integer id and axis-aligned bounding box. This is the leaf data actually stored inside a `QTNode<T>` — the quadtree only ever stores/queries `NodeInfo<T>` entries, never `T` directly, so it can perform spatial overlap tests and removals without touching the entity payload itself.

**Intent:** Wraps the entity id and bounding box alongside the payload so the quadtree can index, move, and spatially test entries without any knowledge of what `T` actually is.

**Use-case:** Created automatically by `QTNode<T>.Insert`/`Update` when inserting entities into a `Quadtree`; retrieved during overlap queries (`QTNode<T>.Retrieve`, `Quadtree.GetCollisionEntitiesAt`) to identify which entities intersect a region.

### ⭐ Constructors

```csharp
public NodeInfo<T>(int id, T info, IntRectangle boundingBox)
```

Creates a `NodeInfo<T>` pairing entity `id` and payload `info` with its spatial `boundingBox`.

**Parameters** \
`id` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`info` [T](../../../) \
`boundingBox` [IntRectangle](../../../Murder/Core/Geometry/IntRectangle.html) \

### ⭐ Properties

#### BoundingBox

```csharp
public readonly Rectangle BoundingBox;
```

The axis-aligned bounding box of the entity, used for spatial overlap tests in the quadtree.

**Returns** \
[Rectangle](../../../Murder/Core/Geometry/Rectangle.html) \

#### EntityInfo

```csharp
public readonly T EntityInfo;
```

The payload associated with this entry — whatever data the caller of `QTNode<T>.Insert` chose to store (e.g. an `Entity`, or a tuple of related component data).

**Returns** \
[T](../../../) \

#### Id

```csharp
public readonly int Id;
```

The entity id this entry was inserted under (typically `Entity.EntityId`). Used by `QTNode<T>` to locate and remove the entry independently of `EntityInfo`.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

⚡
