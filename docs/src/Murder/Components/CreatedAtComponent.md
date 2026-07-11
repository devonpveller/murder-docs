# CreatedAtComponent

**Namespace:** Murder.Components \
**Assembly:** Murder.dll

```csharp
public sealed struct CreatedAtComponent : IComponent
```

Records the game time (in seconds) at which this entity was spawned.

**Implements:** _[IComponent](../../Bang/Components/IComponent.html)_

**Intent:** Provides a reliable creation timestamp so lifetime and cooldown systems can compute how long an entity has existed.

**Use-case:** Added automatically by `CreationTimeSystem`; read by `DestroyAfterSecondsComponent` and other time-based systems to determine when to remove the entity.

### ⭐ Constructors
```csharp
public CreatedAtComponent(float when)
```

**Parameters** \
`when` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

### ⭐ Properties
#### When
```csharp
public float When { get; public set; }
```

The game time, in seconds, at which this entity was created.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \


⚡