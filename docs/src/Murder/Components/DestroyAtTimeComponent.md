# DestroyAtTimeComponent

**Namespace:** Murder.Components \
**Assembly:** Murder.dll

```csharp
public sealed struct DestroyAtTimeComponent : IComponent
```

Schedules an entity for removal (or deactivation) at a specified game time.

**Implements:** _[IComponent](../../Bang/Components/IComponent.html)_

**Intent:** Allows any entity to be automatically cleaned up after a timer expires without needing a dedicated system per entity type.

**Use-case:** Attach to temporary effects, projectiles, or UI popups that should disappear after a fixed duration; set `TimeToDestroy` to the absolute game time of removal and `Style` to control whether the entity is destroyed, deactivated, or has components removed.

### ⭐ Constructors

```csharp
public DestroyAtTimeComponent()
```

Destroy at the end of the frame

```csharp
public DestroyAtTimeComponent(RemoveStyle style, float timeToDestroy)
```

**Parameters** \
`style` [RemoveStyle](../../Murder/Components/RemoveStyle.html) \
`timeToDestroy` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

```csharp
public DestroyAtTimeComponent(float timeToDestroy)
```

**Parameters** \
`timeToDestroy` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

### ⭐ Properties

#### Style

```csharp
public readonly RemoveStyle Style;
```

Determines how the entity is removed once `TimeToDestroy` is reached. `DestroyAtTimeSystem` currently only acts on `Destroy` and `Deactivate`; `RemoveComponents` and `None` result in no action being taken (the `RemoveComponents` case is not yet implemented by the system despite existing on the enum).

**Returns** \
[RemoveStyle](../../Murder/Components/RemoveStyle.html) \

#### TimeToDestroy

```csharp
public readonly float TimeToDestroy;
```

The absolute game time (in seconds) at which the entity should be removed; `-1` means end of current frame.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

⚡
