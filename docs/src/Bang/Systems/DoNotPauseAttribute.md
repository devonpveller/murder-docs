# DoNotPauseAttribute

**Namespace:** Bang.Systems \
**Assembly:** Bang.dll

```csharp
public class DoNotPauseAttribute : Attribute
```

Indicates that a system will not be deactivated when [World.Pause](../../Bang/World.html) is called,
            and will keep running normally until [World.Resume](../../Bang/World.html). By default, only
            [IUpdateSystem](../../Bang/Systems/IUpdateSystem.html) and [IFixedUpdateSystem](../../Bang/Systems/IFixedUpdateSystem.html) systems are eligible to be
            automatically paused in the first place (render, reactive, messager, startup and exit
            systems are never touched by pausing); this attribute opts an otherwise-pausable update
            system out of that behavior, which is useful for logic that must keep ticking while the
            game is paused, such as reading input for a pause menu. If a system also carries
            [IncludeOnPauseAttribute](../../Bang/Systems/IncludeOnPauseAttribute.html), that attribute takes priority and the system will be
            paused anyway. See also [OnPauseAttribute](../../Bang/Systems/OnPauseAttribute.html) for the opposite need - a system
            that should run *only* while paused.

**Implements:** _[Attribute](https://learn.microsoft.com/en-us/dotnet/api/System.Attribute?view=net-7.0)_

### ⭐ Constructors
```csharp
public DoNotPauseAttribute()
```

### ⭐ Properties
#### TypeId
```csharp
public virtual Object TypeId { get; }
```

**Returns** \
[Object](https://learn.microsoft.com/en-us/dotnet/api/System.Object?view=net-7.0) \


⚡
