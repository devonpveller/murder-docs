# EntityTrackerComponent

**Namespace:** Murder.Components \
**Assembly:** Murder.dll

```csharp
public sealed struct EntityTrackerComponent : IComponent
```

This is a component used to track other entities within the world.
            action.

**Implements:** _[IComponent](../../Bang/Components/IComponent.html)_

**Intent:** Stores a reference to another entity by ID so this entity's systems can locate and interact with it each frame.

**Use-case:** Attach to a projectile, follower, or targeting entity and point `Target` at the entity it should track; AI or movement systems read this to resolve the target entity from the world.

### ⭐ Constructors
```csharp
public EntityTrackerComponent(int target)
```

**Parameters** \
`target` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

### ⭐ Properties
#### Target
```csharp
public readonly int Target;
```

Id of the target entity.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \


⚡