# CarveComponent

**Namespace:** Murder.Components \
**Assembly:** Murder.dll

```csharp
public sealed struct CarveComponent : IComponent
```

This is used for carve components within the map (that will not move a lot and
should be taken into account on pathfinding).
This a tag used when caching information in [Map](../../Murder/Core/Map.html).

**Implements:** _[IComponent](../../Bang/Components/IComponent.html)_

**Intent:** Marks a stationary entity as a pathfinding obstacle (or path-opener) so the map cache knows to update the navigation grid around it.

**Use-case:** Attach to walls, furniture, or bridge entities that do not move every frame; the pathfinding system bakes their influence into the navigation grid rather than re-computing it live.

### ⭐ Constructors

```csharp
public CarveComponent()
```

```csharp
public CarveComponent(bool blockVision, bool obstacle, bool clearPath, int weight)
```

**Parameters** \
`blockVision` [bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
`obstacle` [bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
`clearPath` [bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
`weight` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

### ⭐ Properties

#### ApplyLayers

```csharp
public readonly int? ApplyLayers;
```

Optional bitmask of [CollisionLayersBase](../../Murder/Core/Physics/CollisionLayersBase.html) values that are added to the tile(s) this entity occupies, regardless of the `ClearPath` setting. Use this to make a carve entity contribute extra collision layers to the map cache (for example, marking a tile as `PATHFIND`-only) instead of just blocking or clearing it.

**Returns** \
[int?](https://learn.microsoft.com/en-us/dotnet/api/System.Nullable-1?view=net-7.0) \

#### BlockVision

```csharp
public readonly bool BlockVision;
```

When `true`, this entity blocks line-of-sight checks in addition to blocking movement.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### CarveClearPath

```csharp
public static CarveComponent CarveClearPath { get; }
```

Convenience factory that returns a `CarveComponent` pre-configured as a "clear path" carve (`obstacle: false`, `clearPath: true`, `weight: 1`). Use this instead of hand-rolling the constructor when marking bridges, doors, or other tiles that should re-open a path across an otherwise blocked area.

**Returns** \
[CarveComponent](../../Murder/Components/CarveComponent.html) \

#### ClearLayers

```csharp
public readonly int? ClearLayers;
```

Optional bitmask of [CollisionLayersBase](../../Murder/Core/Physics/CollisionLayersBase.html) values to remove from the tile(s) this entity occupies. Only honored when `ClearPath` is `true`; when `ClearPath` is `false`, all collision layers on the covered tiles are cleared instead. Use this to reopen only specific layers (e.g. clear `SOLID` but keep `PATHFIND` blocked) on a bridge-like carve.

**Returns** \
[int?](https://learn.microsoft.com/en-us/dotnet/api/System.Nullable-1?view=net-7.0) \

#### ClearPath

```csharp
public readonly bool ClearPath;
```

Whether this carve component will add a path if there was previously a collision in its area.
For example, a bridge over a river.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### Obstacle

```csharp
public readonly bool Obstacle;
```

When `true`, this entity is treated as an impassable obstacle on the navigation grid.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### Weight

```csharp
public readonly int Weight;
```

Weight of the component, if not an obstacle.
Ignored if [CarveComponent.Obstacle](../../Murder/Components/CarveComponent.html#obstacle) is true.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

### ⭐ Methods

#### WithClearPath(bool)

```csharp
public CarveComponent WithClearPath(bool clearPath)
```

Returns a copy of this component with `ClearPath` set to `clearPath`.

**Parameters** \
`clearPath` [bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

**Returns** \
[CarveComponent](../../Murder/Components/CarveComponent.html) \

⚡
