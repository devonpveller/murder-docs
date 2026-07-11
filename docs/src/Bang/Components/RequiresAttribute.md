# RequiresAttribute

**Namespace:** Bang.Components \
**Assembly:** Bang.dll

```csharp
public class RequiresAttribute : Attribute
```

Marks a component as requiring other components when being added to an entity.
            This is an attribute that tells that a given data requires another one of the same type.
            For example: a component requires another component when adding it to the entity,
            or a system requires another system when adding it to a world.
            If this is for a system, it assumes that the system that depends on the other one comes first.

When `World.DIAGNOSTICS_MODE` is enabled, every time an entity is activated in the world Bang walks
its components and, for each one decorated with `[Requires(typeof(X), typeof(Y), ...)]`, asserts
that the entity also has an `X` and a `Y` component. This turns missing-dependency bugs (a
component whose logic implicitly assumes another component exists on the same entity) into an
immediate, loud failure in development builds instead of a subtle runtime `NullReferenceException`
or silently-wrong behavior later on. The check is forgiving in one specific way: if a required
component type itself has a [GeneratesAttribute](../../Bang/Components/GeneratesAttribute.html)
pointing at another component, and the entity has *that* generated component instead of the
originally required one, the requirement still counts as satisfied. In the Murder engine this is
used, for instance, to declare that `SpriteComponent` requires a
[PositionComponent](../../Bang/Components/PositionComponent.html)
(`src\Murder\Components\Graphics\SpriteComponent.cs`), or that `AgentSpriteComponent` requires a
`FacingComponent` (`src\Murder\Components\Agents\AgentSpriteComponent.cs`) — documenting, and
enforcing, an implicit composition contract between components. The same attribute can also be
applied to a [ISystem](../../Bang/Systems/ISystem.html) to declare that it must be registered after
another system in the same world.

**Implements:** _[Attribute](https://learn.microsoft.com/en-us/dotnet/api/System.Attribute?view=net-7.0)_

### ⭐ Constructors
```csharp
public RequiresAttribute(Type[] types)
```

Creates a new [RequiresAttribute](../../Bang/Components/RequiresAttribute.html).

**Parameters** \
`types` [Type[]](https://learn.microsoft.com/en-us/dotnet/api/System.Type?view=net-7.0) \
\

### ⭐ Properties
#### TypeId
```csharp
public virtual Object TypeId { get; }
```

**Returns** \
[Object](https://learn.microsoft.com/en-us/dotnet/api/System.Object?view=net-7.0) \
#### Types
```csharp
public Type[] Types { get; public set; }
```

System will target all entities that have this set of components.

**Returns** \
[Type[]](https://learn.microsoft.com/en-us/dotnet/api/System.Type?view=net-7.0) \


⚡