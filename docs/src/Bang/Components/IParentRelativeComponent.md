# IParentRelativeComponent

**Namespace:** Bang.Components \
**Assembly:** Bang.dll

```csharp
public abstract IParentRelativeComponent : IComponent
```

A component that is relative to the parent.
            It will be notified each time the tracking component of the parent changes.

Bang entities can be parented to one another (see `Entity.SetParent`). When a component on the
parent entity implements `IParentRelativeComponent` and the child entity has a component of the
same type, the engine keeps the child's value in sync with the parent automatically: any time the
parent's component is replaced, the engine calls `OnParentModified` on the child's component so it
can recompute itself relative to the new parent value, then writes the result back onto the child
via `Entity.ReplaceComponent`. This is how, for example, moving a parent entity also moves all of
its children without every system needing to know about the parent/child relationship explicitly.
[PositionComponent](../../Bang/Components/PositionComponent.html) is the canonical implementation:
its `X`/`Y` are always the position *relative* to the parent, `HasParent` reports whether it is
currently tracking one, and `OnParentModified` adds the parent's resolved global position to the
child's local offset and writes the combined global position back onto the child.

`WithoutParent` is used when an entity is reparented or unparented — it returns a copy of the
component with the parent-relative bookkeeping cleared (for `PositionComponent`, this discards the
cached global position and keeps only the local X/Y), so the component reverts to being
interpreted as absolute/local again. Implement this interface on a component when its meaning
should change automatically as its entity's parent changes; components representing values that
are always absolute (independent of hierarchy) should just implement plain
[IComponent](../../Bang/Components/IComponent.html) instead.

**Implements:** _[IComponent](../../Bang/Components/IComponent.html)_

### ⭐ Properties
#### HasParent
```csharp
public abstract virtual bool HasParent { get; }
```

Whether the component has a parent that it's tracking.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
### ⭐ Methods
#### WithoutParent()
```csharp
public abstract IParentRelativeComponent WithoutParent()
```

Creates a copy of the component without any parent.

**Returns** \
[IParentRelativeComponent](../../Bang/Components/IParentRelativeComponent.html) \

#### OnParentModified(IComponent, Entity)
```csharp
public abstract void OnParentModified(IComponent parentComponent, Entity childEntity)
```

Called when a parent modifies <paramref name="parentComponent" />.

**Parameters** \
`parentComponent` [IComponent](../../Bang/Components/IComponent.html) \
\
`childEntity` [Entity](../../Bang/Entities/Entity.html) \
\



⚡