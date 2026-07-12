# QuadtreeComponent

**Namespace:** Murder.Components \
**Assembly:** Murder.dll

```csharp
public sealed struct QuadtreeComponent : IModifiableComponent, IComponent
```

Singleton component that owns the world's [Quadtree](../../Murder/Core/Physics/Quadtree.html), the broad-phase spatial index used for collision and push-away queries. Only one instance exists per world.

**Intent:** Provide fast spatial look-up of entities within rectangular regions without every system having to iterate all entities manually.

**Use-case:** Created lazily by `Quadtree.GetOrCreateUnique` the first time a system asks for the world's quadtree, sized to the map bounds, and kept up to date by `QuadtreeCalculatorSystem` as entities with `PositionComponent` and [ColliderComponent](../../Murder/Components/ColliderComponent.html) are added, moved, or removed. It is marked `[RuntimeOnly]` and `[DoNotPersistEntityOnSave]` because the quadtree is a derived, in-memory acceleration structure that must never be serialized to save files or world assets.

**Implements:** _[IModifiableComponent](../../Bang/Components/IModifiableComponent.html), [IComponent](../../Bang/Components/IComponent.html)_

### ⭐ Constructors

```csharp
public QuadtreeComponent(Rectangle size)
```

Creates a new quadtree component whose spatial index covers `size`, typically the map's bounding box.

**Parameters** \
`size` [Rectangle](../../Murder/Core/Geometry/Rectangle.html) \

### ⭐ Properties

#### Quadtree

```csharp
public readonly Quadtree Quadtree;
```

The underlying quadtree data structure used to spatially index entities in the world for collision and push-away queries.

**Returns** \
[Quadtree](../../Murder/Core/Physics/Quadtree.html) \

### ⭐ Methods

#### Subscribe(Action)

```csharp
public virtual void Subscribe(Action notification)
```

No-op implementation of `IModifiableComponent.Subscribe`; the quadtree is mutated in place and does not raise change notifications to subscribers.

**Parameters** \
`notification` [Action](https://learn.microsoft.com/en-us/dotnet/api/System.Action?view=net-7.0) \

#### Unsubscribe(Action)

```csharp
public virtual void Unsubscribe(Action notification)
```

No-op implementation of `IModifiableComponent.Unsubscribe`; there is nothing to unsubscribe from since the quadtree never raises change notifications.

**Parameters** \
`notification` [Action](https://learn.microsoft.com/en-us/dotnet/api/System.Action?view=net-7.0) \

⚡
