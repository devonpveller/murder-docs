# QTNode\<T\>

**Namespace:** Murder.Core.Physics \
**Assembly:** Murder.dll

```csharp
public class QTNode<T>
```

A single node in a spatial quadtree, holding entity bounding-box data and up to four child sub-nodes that subdivide its rectangular bounds.

**Intent:** Internal quadtree node that stores entities whose bounding boxes overlap its `Bounds` rectangle, splitting into child nodes when capacity is exceeded.

**Use-case:** Not used directly; interact with the quadtree through `Quadtree` methods such as `GetCollisionEntitiesAt` and `AddToCollisionQuadTree`.

### ⭐ Constructors
```csharp
public QTNode<T>(int level, Rectangle bounds)
```

Creates a quadtree node at the given subdivision `level` covering the specified `bounds` rectangle.

**Parameters** \
`level` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`bounds` [Rectangle](../../../Murder/Core/Geometry/Rectangle.html) \

### ⭐ Properties
#### Bounds
```csharp
public readonly Rectangle Bounds;
```

The world-space rectangle this node covers.

**Returns** \
[Rectangle](../../../Murder/Core/Geometry/Rectangle.html) \
#### Entities
```csharp
public readonly Dictionary<TKey, TValue> Entities;
```

Entities are indexed by their entity ID number

**Returns** \
[Dictionary\<TKey, TValue\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Generic.Dictionary-2?view=net-7.0) \
#### Level
```csharp
public readonly int Level;
```

The subdivision depth of this node; 0 is the root.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
#### Nodes
```csharp
public ImmutableArray<T> Nodes;
```

The four child sub-nodes created when this node is subdivided. Empty until subdivision occurs.

**Returns** \
[ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \
### ⭐ Methods
#### Remove(int)
```csharp
public bool Remove(int entityId)
```

Removes an entity from the quadtree

**Parameters** \
`entityId` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
\

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
\

#### Clear()
```csharp
public void Clear()
```

Recursively clears all entities of the node, but keeps the structure

#### DrawDebug(Batch2D)
```csharp
public void DrawDebug(Batch2D spriteBatch)
```

Draws the node's bounding rectangle and entity outlines to `spriteBatch` for debugging purposes.

**Parameters** \
`spriteBatch` [Batch2D](../../../Murder/Core/Graphics/Batch2D.html) \

#### Insert(int, T, Rectangle)
```csharp
public void Insert(int entityId, T info, Rectangle boundingBox)
```

**Parameters** \
`entityId` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`info` [T](../../../) \
`boundingBox` [Rectangle](../../../Murder/Core/Geometry/Rectangle.html) \

#### Reset()
```csharp
public void Reset()
```

Completely resets the node removing anything inside

#### Retrieve(Rectangle, List<T>)
```csharp
public void Retrieve(Rectangle boundingBox, List<T> returnEntities)
```

**Parameters** \
`boundingBox` [Rectangle](../../../Murder/Core/Geometry/Rectangle.html) \
`returnEntities` [List\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Generic.List-1?view=net-7.0) \

#### Split()
```csharp
public void Split()
```



⚡