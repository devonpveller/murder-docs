# ParallaxComponent

**Namespace:** Murder.Components.Graphics \
**Assembly:** Murder.dll

```csharp
public sealed struct ParallaxComponent : IComponent
```

Controls how much an entity's rendered position is offset relative to the camera, creating a depth-based parallax scrolling effect.

**Intent:** Give background and foreground layers a sense of depth by making them move at a different rate than world-space entities.

**Use-case:** Add to background sprite entities and set `Factor` below 1 (e.g. 0.5) for distant layers that move slowly, or above 1 for foreground layers that move faster than the camera.

**Implements:** _[IComponent](../../../Bang/Components/IComponent.html)_

### ⭐ Constructors
```csharp
public ParallaxComponent()
```

### ⭐ Properties
#### Factor
```csharp
public readonly float Factor;
```

How much parallax this entity has. 0 never moves, 1 moves normaly and more than 1 is the foreground.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \


⚡