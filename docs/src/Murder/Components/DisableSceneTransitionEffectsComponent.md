# DisableSceneTransitionEffectsComponent

**Namespace:** Murder.Components \
**Assembly:** Murder.dll

```csharp
public sealed struct DisableSceneTransitionEffectsComponent : IComponent
```

Component that will disable any transition effects between scenes.

**Implements:** _[IComponent](../../Bang/Components/IComponent.html)_

**Intent:** Suppresses the default fade/wipe transition when loading into a new scene, allowing for instant or custom scene switches.

**Use-case:** Attach to the world entity before a scene change when a cutscene or gameplay system needs a seamless transition without fade effects; optionally set `OverrideCameraPosition` to snap the camera to a specific position on arrival.

### ⭐ Constructors
```csharp
public DisableSceneTransitionEffectsComponent()
```

```csharp
public DisableSceneTransitionEffectsComponent(Vector2 bounds)
```

**Parameters** \
`bounds` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

### ⭐ Properties
#### OverrideCameraPosition
```csharp
public readonly T? OverrideCameraPosition;
```

Optional world-space position that the camera should be snapped to when the transition completes, bypassing the normal camera follow initialization.

**Returns** \
[T?](https://learn.microsoft.com/en-us/dotnet/api/System.Nullable-1?view=net-7.0) \


⚡