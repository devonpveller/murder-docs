# NodeInfo\<T\>

**Namespace:** Murder.Core.Physics \
**Assembly:** Murder.dll

```csharp
public sealed struct NodeInfo<T>
```

Pairs an entity payload `T` with its axis-aligned bounding box, used as the leaf data stored in `QTNode<T>` entries.

**Intent:** Wraps the bounding box alongside the entity data so the quadtree can perform spatial overlap tests without accessing the entity itself.

**Use-case:** Created automatically when inserting entities into a `Quadtree`; retrieved during overlap queries to identify which entities intersect a region.

### ⭐ Constructors
```csharp
public NodeInfo<T>(T info, Rectangle boundingBox)
```

Creates a `NodeInfo` pairing the entity data `info` with its spatial bounding box.

**Parameters** \
`info` [T](../../../) \
`boundingBox` [Rectangle](../../../Murder/Core/Geometry/Rectangle.html) \

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

The entity payload (e.g., an entity ID or component snapshot) associated with this node entry.

**Returns** \
[T](../../../) \


⚡