# InCameraComponent

**Namespace:** Murder.Components \
**Assembly:** Murder.dll

```csharp
public sealed struct InCameraComponent : IComponent
```

Runtime marker added to entities that are currently within the camera's visible bounds, storing their computed render position.

**Intent:** Allow render and game systems to quickly determine which entities are on-screen and where they should be drawn without repeating camera projection math.

**Use-case:** Added and removed automatically by camera culling systems; read `RenderPosition` in a render system to obtain the already-projected screen position for this entity.

**Implements:** _[IComponent](../../Bang/Components/IComponent.html)_

### ⭐ Constructors

```csharp
public InCameraComponent(Vector2 renderPosition)
```

**Parameters** \
`renderPosition` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

### ⭐ Properties

#### RenderPosition

```csharp
public readonly Vector2 RenderPosition;
```

The pre-computed screen-space position at which this entity should be rendered this frame.

**Returns** \
[Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

⚡
