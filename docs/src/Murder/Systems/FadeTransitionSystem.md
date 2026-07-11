# FadeTransitionSystem

**Namespace:** Murder.Systems \
**Assembly:** Murder.dll

```csharp
public class FadeTransitionSystem : IUpdateSystem, ISystem, IReactiveSystem
```

System responsible for fading in and out entities.
            This is not responsible for the screen fade transition.

**Intent:** Animates an entity's alpha value from a starting value to a target value over a defined duration using a cubic-out easing curve.

**Use-case:** Attach `FadeTransitionComponent` to any entity you want to fade in or out; set `DestroyEntityOnEnd` to automatically clean up the entity when the animation completes.

**Implements:** _[IUpdateSystem](../../Bang/Systems/IUpdateSystem.html), [ISystem](../../Bang/Systems/ISystem.html), [IReactiveSystem](../../Bang/Systems/IReactiveSystem.html)_

### ⭐ Constructors
```csharp
public FadeTransitionSystem()
```

### ⭐ Methods
#### OnAdded(World, ImmutableArray<T>)
```csharp
public virtual void OnAdded(World world, ImmutableArray<T> entities)
```

Initializes the fade by recording the entity's current alpha as the start value when `FadeTransitionComponent.StartTime` is zero.

**Parameters** \
`world` [World](../../Bang/World.html) \
`entities` [ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \

#### OnModified(World, ImmutableArray<T>)
```csharp
public virtual void OnModified(World world, ImmutableArray<T> entities)
```

No-op; modifications to `FadeTransitionComponent` are handled reactively via `OnAdded`.

**Parameters** \
`world` [World](../../Bang/World.html) \
`entities` [ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \

#### OnRemoved(World, ImmutableArray<T>)
```csharp
public virtual void OnRemoved(World world, ImmutableArray<T> entities)
```

No-op; removal is self-managed by `Update` when the fade duration expires.

**Parameters** \
`world` [World](../../Bang/World.html) \
`entities` [ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \

#### Update(Context)
```csharp
public virtual void Update(Context context)
```

Evaluates the cubic-out easing curve at the current elapsed time and sets the entity's `AlphaComponent`; removes or destroys the entity when the fade is complete.

**Parameters** \
`context` [Context](../../Bang/Contexts/Context.html) \



⚡