# QTNode\<T\>

**Namespace:** Murder.Core.Physics \
**Assembly:** Murder.dll

```csharp
public class QTNode<T>
```

A single node in a spatial quadtree (loosely based on the classic tutsplus quadtree tutorial), holding entity bounding-box data (`NodeInfo<T>`) and up to four child sub-nodes that subdivide its rectangular bounds once it exceeds capacity.

**Intent:** Internal quadtree node that stores entries whose bounding boxes overlap its bounds, splitting into four child nodes when it exceeds 32 entries (up to 6 levels deep).

**Use-case:** Not used directly; game code does not usually construct or walk a `QTNode<T>` — it is the storage backing `Quadtree`'s collision, push-away, and static-render partitions, accessed through that class's helper methods such as `GetCollisionEntitiesAt` and `AddToCollisionQuadTree`.

### ⭐ Constructors

```csharp
public QTNode<T>(int level, IntRectangle bounds)
```

Creates the root node of a quadtree at subdivision `level` 0, covering `bounds`. Also allocates the entity-id-to-node lookup table shared by the whole tree, which is what makes `Remove` and `Update` O(1) instead of requiring a recursive search. Always pass `level: 0` here — this constructor is only meant for the root; children are created internally when a node splits.

**Parameters** \
`level` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`bounds` [IntRectangle](../../../Murder/Core/Geometry/IntRectangle.html) \

### ⭐ Properties

#### _entities

```csharp
public readonly Dictionary<TKey, TValue> _entities;
```

The entries stored directly on this node (not in a child), indexed by their entity ID number. This field is public for historical reasons but keeps the underscore-prefixed private-style name; it is not intended to be mutated from outside `QTNode<T>` — use `Insert`, `Update`, and `Remove` instead.

**Returns** \
[Dictionary\<TKey, TValue\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Generic.Dictionary-2?view=net-7.0) \

### ⭐ Methods

#### Remove(int)

```csharp
public bool Remove(int entityId)
```

Removes an entity from the quadtree using the root's O(1) entity-id-to-node lookup — must be called on the root node (the one constructed with `level == 0`), since only the root owns the lookup table. Does nothing and returns `false` if the entity is not present.

**Parameters** \
`entityId` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### Clear()

```csharp
public void Clear()
```

Recursively clears all entities of the node, but keeps the structure

#### DrawDebug(Batch2D)

```csharp
public void DrawDebug(Batch2D spriteBatch)
```

Recursively draws this node's bounds (colored by subdivision depth) and the number of entities it directly holds to `spriteBatch`, then recurses into any child nodes. Used exclusively by editor/debug rendering to visualize how the quadtree has subdivided.

**Parameters** \
`spriteBatch` [Batch2D](../../../Murder/Core/Graphics/Batch2D.html) \

#### Insert(int, T, Rectangle)

```csharp
public void Insert(int entityId, T info, Rectangle boundingBox)
```

Insert the object into the quadtree. If the node exceeds the capacity, it will split and add all objects to their corresponding nodes.

**Parameters** \
`entityId` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`info` [T](../../../) \
`boundingBox` [Rectangle](../../../Murder/Core/Geometry/Rectangle.html) \

#### Reset()

```csharp
public void Reset()
```

Completely resets the node removing anything inside

#### Retrieve(Rectangle, List<NodeInfo<T>>)

```csharp
public void Retrieve(Rectangle boundingBox, List<NodeInfo<T>> results)
```

Return all objects that could collide with the given object at `results`.

**Parameters** \
`boundingBox` [Rectangle](../../../Murder/Core/Geometry/Rectangle.html) \
`results` [List\<NodeInfo\<T\>\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Generic.List-1?view=net-7.0) \

#### Update(int, T, Rectangle)

```csharp
public void Update(int entityId, T info, Rectangle newBounds)
```

Updates an existing entity's payload and bounding box in place. If the entity still fits within its current node's bounds, this is a cheap in-place replace; otherwise the entry is removed and re-inserted from the root, which may move it to a different node (or trigger a split). Must be called on the root node, since it relies on the shared entity-id-to-node lookup like `Remove`. If the entity is not currently tracked, this behaves like a plain `Insert`.

**Parameters** \
`entityId` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`info` [T](../../../) \
`newBounds` [Rectangle](../../../Murder/Core/Geometry/Rectangle.html) \

⚡
