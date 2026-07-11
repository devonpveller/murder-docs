# IntrinsicAttribute

**Namespace:** Bang.Attributes \
**Assembly:** Bang.dll

```csharp
public class IntrinsicAttribute : Attribute
```

This signalizes that a component is an intrinsic characteristic of the entity and
            that it does not distinct as a separate entity.
            An entity with only intrinsic components will not be serialized.

`[Intrinsic]` marks a component as being such a fundamental, universal trait of an entity that its
mere presence should not, by itself, make the entity "count" as meaningful game data. Concretely,
`EntityInstance.HasNonIntrinsicComponent()` (`src\Murder\Data\Prefabs\EntityInstance.cs`) walks an
entity's component types and checks each one with `Attribute.IsDefined(t, typeof(IntrinsicAttribute))`;
if every single component on the entity is intrinsic, the entity is treated as having no
distinguishing data of its own and is skipped during serialization. The prototypical example is
[PositionComponent](../../Bang/Components/PositionComponent.html), which is decorated with
`[Intrinsic]` in `bang\src\Bang\Components\PositionComponent.cs` — nearly every entity has a
position, so an entity that has *only* a position and nothing else is not worth persisting as a
standalone entity.

Note this type physically lives in `bang\src\Bang\Components\IntrinsicAttribute.cs` but declares
`namespace Bang.Attributes`, not `Bang.Components` — despite the source file's location, the type
itself belongs to the `Bang.Attributes` namespace, so `using Bang.Attributes;` is required to
reference it (see the `using` at the top of `PositionComponent.cs`). Apply `[Intrinsic]` to any new
component that represents a baseline trait nearly all entities share and that alone should never be
enough to justify serializing an otherwise-empty entity.

**Implements:** _[Attribute](https://learn.microsoft.com/en-us/dotnet/api/System.Attribute?view=net-7.0)_

### ⭐ Constructors
```csharp
public IntrinsicAttribute()
```

Creates a new [IntrinsicAttribute](../../Bang/Attributes/IntrinsicAttribute.html).

### ⭐ Properties
#### TypeId
```csharp
public virtual Object TypeId { get; }
```

**Returns** \
[Object](https://learn.microsoft.com/en-us/dotnet/api/System.Object?view=net-7.0) \


⚡