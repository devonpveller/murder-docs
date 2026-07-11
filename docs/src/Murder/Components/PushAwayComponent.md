# PushAwayComponent

**Namespace:** Murder.Components \
**Assembly:** Murder.dll

```csharp
public sealed struct PushAwayComponent : IComponent
```

Causes an entity to repel other nearby entities within a defined radius each frame.

**Intent:** Implement simple push-away collision response so entities don't overlap.

**Use-case:** Attach to an enemy or NPC to make it push away other characters that enter its bounding radius; tune `Size` for the area of influence and `Strength` for how forcefully others are repelled.

**Implements:** _[IComponent](../../Bang/Components/IComponent.html)_

### ⭐ Constructors
```csharp
public PushAwayComponent(int size, int strength)
```

**Parameters** \
`size` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`strength` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

### ⭐ Properties
#### Size
```csharp
public readonly float Size;
```

Diameter of the push-away area around the entity's position.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
#### Strength
```csharp
public readonly float Strength;
```

Force magnitude applied to nearby entities to push them away.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
### ⭐ Methods
#### GetBoundingBox(IMurderTransformComponent)
```csharp
public Rectangle GetBoundingBox(IMurderTransformComponent position)
```

Returns the push-away bounding box centered on the given transform position.

**Parameters** \
`position` [IMurderTransformComponent](../../Murder/Components/IMurderTransformComponent.html) \

**Returns** \
[Rectangle](../../Murder/Core/Geometry/Rectangle.html) \

#### GetBoundingBox(Vector2)
```csharp
public Rectangle GetBoundingBox(Vector2 position)
```

Returns the push-away bounding box centered on the given world position.

**Parameters** \
`position` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

**Returns** \
[Rectangle](../../Murder/Core/Geometry/Rectangle.html) \



⚡