# VerticalPositionComponent

**Namespace:** Murder.Components \
**Assembly:** Murder.dll

```csharp
public sealed struct VerticalPositionComponent : IComponent
```

Tracks the vertical (Z-axis) position and velocity of an entity in a top-down 2.5D game. The entity can be above the ground and optionally subject to gravity.

**Intent:** Add a height dimension to 2D entities without a full 3D transform.

**Use-case:** Attach to characters or objects that can jump or be thrown; set `HasGravity` to apply the built-in constant gravity, or false for floating objects.

**Implements:** _[IComponent](../../Bang/Components/IComponent.html)_

### ⭐ Constructors
```csharp
public VerticalPositionComponent()
```

```csharp
public VerticalPositionComponent(float z, float zVelocity, bool hasGravity)
```

**Parameters** \
`z` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`zVelocity` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`hasGravity` [bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

### ⭐ Properties
#### GRAVITY
```csharp
public static const float GRAVITY;
```

Base gravity constant (0.1) used as the acceleration multiplier each frame.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
#### HasGravity
```csharp
public readonly bool HasGravity;
```

When true, gravity is applied to `ZVelocity` each frame, pulling the entity toward the ground.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
#### Z
```csharp
public readonly float Z;
```

Current vertical height above the ground in pixels (0 = on the ground).

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
#### ZVelocity
```csharp
public readonly float ZVelocity;
```

Current vertical velocity in pixels per second; negative values move toward the ground.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
### ⭐ Methods
#### UpdatePosition(float, float)
```csharp
public VerticalPositionComponent UpdatePosition(float deltaTime, float bounciness)
```

Advances the vertical physics simulation by one frame, applying gravity and bounce.

**Parameters** \
`deltaTime` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`bounciness` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

**Returns** \
[VerticalPositionComponent](../../Murder/Components/VerticalPositionComponent.html) \



⚡