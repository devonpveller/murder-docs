# PathfindGridComponent

**Namespace:** Murder.Components \
**Assembly:** Murder.dll

```csharp
public sealed struct PathfindGridComponent : IComponent
```

Stores per-cell pathfinding overrides (weights and collision masks) that the pathfinding system layers on top of the default tile map.

**Intent:** Allow level designers to fine-tune pathfinding cost and passability for specific grid cells without modifying the tile asset.

**Use-case:** Add to the world entity (`[Unique]`) and populate `Cells` via the editor to mark heavy or impassable areas; the pathfinding system reads these properties when building traversal costs.

**Implements:** _[IComponent](../../Bang/Components/IComponent.html)_

### ⭐ Constructors
```csharp
public PathfindGridComponent()
```

```csharp
public PathfindGridComponent(ImmutableArray<T> cells)
```

**Parameters** \
`cells` [ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \

### ⭐ Properties
#### Cells
```csharp
public readonly ImmutableArray<T> Cells;
```

Unique collection of cell properties. "How do we keep this unique", you ask?
            This is responsability of the editor editing this. This cannot be a dictionary (I would love to!)
            because it will break the deterministic behavior of the world.

**Returns** \
[ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \


⚡