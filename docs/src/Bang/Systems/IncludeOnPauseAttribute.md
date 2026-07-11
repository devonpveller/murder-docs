# IncludeOnPauseAttribute

**Namespace:** Bang.Systems \
**Assembly:** Bang.dll

```csharp
public class IncludeOnPauseAttribute : Attribute
```

Forces a system to be included in the set of systems that get deactivated when
            [World.Pause](../../Bang/World.html) is called (and reactivated on [World.Resume](../../Bang/World.html)),
            regardless of what kind of [ISystem](../../Bang/Systems/ISystem.html) it is. By default only
            [IUpdateSystem](../../Bang/Systems/IUpdateSystem.html) and [IFixedUpdateSystem](../../Bang/Systems/IFixedUpdateSystem.html) systems are ever
            automatically paused; this attribute is what you reach for to pause a system that would
            not normally qualify (e.g. an [IReactiveSystem](../../Bang/Systems/IReactiveSystem.html) or [IMessagerSystem](../../Bang/Systems/IMessagerSystem.html)
            that should stop reacting while the game is paused). This will override
            [DoNotPauseAttribute](../../Bang/Systems/DoNotPauseAttribute.html) - if a system carries both, it will still be paused.

**Implements:** _[Attribute](https://learn.microsoft.com/en-us/dotnet/api/System.Attribute?view=net-7.0)_

### ⭐ Constructors
```csharp
public IncludeOnPauseAttribute()
```

### ⭐ Properties
#### TypeId
```csharp
public virtual Object TypeId { get; }
```

**Returns** \
[Object](https://learn.microsoft.com/en-us/dotnet/api/System.Object?view=net-7.0) \


⚡
