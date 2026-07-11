# QuadtreeComponent

**Namespace:** Murder.Components \
**Assembly:** Murder.dll

```csharp
public sealed struct QuadtreeComponent : IModifiableComponent, IComponent
```

Singleton component that holds the spatial quadtree used for broad-phase collision and entity queries. Only one instance exists per world.

**Intent:** Provide fast spatial look-up of entities within rectangular regions.

**Use-case:** Added automatically by the engine when a world is initialised; call physics services that accept a `Quadtree` to query nearby entities instead of iterating all entities manually.

**Implements:** _[IModifiableComponent](../../Bang/Components/IModifiableComponent.html), [IComponent](../../Bang/Components/IComponent.html)_

### ⭐ Constructors
```csharp
public QuadtreeComponent(Rectangle size)
```

**Parameters** \
`size` [Rectangle](../../Murder/Core/Geometry/Rectangle.html) \

### ⭐ Properties
#### Quadtree
```csharp
public readonly Quadtree Quadtree;
```

The underlying quadtree data structure used to spatially index entities in the world.

**Returns** \
[Quadtree](../../Murder/Core/Physics/Quadtree.html) \
### ⭐ Methods
#### Subscribe(Action)
```csharp
public virtual void Subscribe(Action notification)
```

No-op; the quadtree does not raise change notifications.

**Parameters** \
`notification` [Action](https://learn.microsoft.com/en-us/dotnet/api/System.Action?view=net-7.0) \

#### Unsubscribe(Action)
```csharp
public virtual void Unsubscribe(Action notification)
```

No-op; the quadtree does not raise change notifications.

**Parameters** \
`notification` [Action](https://learn.microsoft.com/en-us/dotnet/api/System.Action?view=net-7.0) \



⚡