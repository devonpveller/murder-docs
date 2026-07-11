# OnPauseAttribute

**Namespace:** Bang.Systems \
**Assembly:** Bang.dll

```csharp
public class OnPauseAttribute : Attribute
```

Indicates that a system should run *only* while the world is paused. A system carrying
            this attribute starts deactivated when the [World](../../Bang/World.html) is built; it is
            automatically activated when [World.Pause](../../Bang/World.html) runs and deactivated again on the
            following [World.Resume](../../Bang/World.html). This is the mirror image of
            [DoNotPauseAttribute](../../Bang/Systems/DoNotPauseAttribute.html) (which keeps a system running always, pause or not) and
            is meant for systems whose entire purpose is tied to the paused state - e.g. driving a
            pause menu's animations or input while the rest of gameplay is frozen.

**Implements:** _[Attribute](https://learn.microsoft.com/en-us/dotnet/api/System.Attribute?view=net-7.0)_

### ⭐ Constructors
```csharp
public OnPauseAttribute()
```

### ⭐ Properties
#### TypeId
```csharp
public virtual Object TypeId { get; }
```

**Returns** \
[Object](https://learn.microsoft.com/en-us/dotnet/api/System.Object?view=net-7.0) \


⚡
