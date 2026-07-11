# AgentSpriteComponent

**Namespace:** Murder.Components \
**Assembly:** Murder.dll

```csharp
public sealed struct AgentSpriteComponent : IComponent
```

Configures which sprite asset and animation name prefixes an agent entity uses for idle and walk states.

**Implements:** _[IComponent](../../Bang/Components/IComponent.html)_

**Intent:** Links an agent entity to a sprite asset and defines the naming convention for its directional idle/walk animation clips.

**Use-case:** Attach to any entity with an `AgentComponent` and `FacingComponent`; `AgentSpriteSystem` reads this to play the correct animation depending on whether the agent is moving or idle.

### ⭐ Constructors
```csharp
public AgentSpriteComponent()
```

### ⭐ Properties
#### AnimationGuid
```csharp
public Guid AnimationGuid { get; public set; }
```

GUID of the `SpriteAsset` that contains the agent's animations.

**Returns** \
[Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \
#### IdlePrefix
```csharp
public readonly string IdlePrefix;
```

Prefix used to look up the idle animation clips (e.g., `"idle"` matches `"idle_right"`, `"idle_up"`, etc.).

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
#### TargetSpriteBatch
```csharp
public readonly int TargetSpriteBatch;
```

Index of the sprite batch that this agent's sprite is rendered into.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
#### WalkPrefix
```csharp
public readonly string WalkPrefix;
```

Prefix used to look up the walk animation clips (e.g., `"walk"` matches `"walk_right"`, `"walk_up"`, etc.).

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
#### YSortOffset
```csharp
public readonly int YSortOffset;
```

Vertical pixel offset added to this entity's Y position when computing draw-order sorting.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \


⚡