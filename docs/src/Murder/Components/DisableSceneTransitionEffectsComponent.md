# DisableSceneTransitionEffectsComponent

**Namespace:** Murder.Components \
**Assembly:** Murder.dll

```csharp
public sealed struct DisableSceneTransitionEffectsComponent : IComponent
```

Component that will disable any transition effects between scenes.

**Implements:** _[IComponent](../../Bang/Components/IComponent.html)_

**Intent:** Suppresses scene-transition-only behavior — most concretely, it lets `StaticInCameraSystem` compute which static entities are visible using a forced camera rectangle instead of the real camera bounds, which is useful the moment a new scene loads and the camera hasn't caught up to its target yet. `[Unique]` means only one instance can exist on the world at a time.

**Use-case:** Add to the world entity right after loading a new scene (or right before a scene transition) when static/quadtree visibility, camera offsets, or pending transition cleanup need to bypass their normal steady-state logic for that one transition. `ForceCameraPosition` is read directly by `StaticInCameraSystem` to reposition the safe-bounds query used to mark static sprites as in-camera; `PlayerOffsetFromCamera`, `PlayerOffsetFromTarget`, and `CleanUpAnyPendingOnes` are transition bookkeeping fields intended for scene/camera-follow code that needs to know the offset the player had relative to the camera or follow target, and whether any pending transition effects should be discarded, during the transition window.

### ⭐ Constructors

```csharp
public DisableSceneTransitionEffectsComponent()
```

Creates the component with no forced camera position and `CleanUpAnyPendingOnes` set to `false`.

```csharp
public DisableSceneTransitionEffectsComponent(Vector2 bounds)
```

Creates the component with `ForceCameraPosition` set to `bounds`, forcing static-visibility queries to use this position instead of the live camera position.

**Parameters** \
`bounds` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

```csharp
public DisableSceneTransitionEffectsComponent(bool cleanUpAnyPendingOnes)
```

Creates the component with no forced camera position, explicitly setting whether any pending transition effects should be cleaned up.

**Parameters** \
`cleanUpAnyPendingOnes` [bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

### ⭐ Properties

#### CleanUpAnyPendingOnes

```csharp
public readonly bool CleanUpAnyPendingOnes;
```

When `true`, any transition effects still pending from a previous scene should be discarded rather than allowed to finish, so the new scene starts in a clean state.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### ForceCameraPosition

```csharp
public readonly Vector2? ForceCameraPosition;
```

Optional world-space position used in place of the live camera position when computing which static entities are currently visible. `StaticInCameraSystem` reads this to reposition its safe-bounds query, which is useful right after a scene load when the real camera hasn't yet settled on its target.

**Returns** \
[Vector2?](https://learn.microsoft.com/en-us/dotnet/api/System.Nullable-1?view=net-7.0) \

#### PlayerOffsetFromCamera

```csharp
public readonly Vector2? PlayerOffsetFromCamera;
```

Optional offset between the player entity and the camera at the moment the transition began, preserved so camera-follow logic can restore the same relative framing after the transition completes.

**Returns** \
[Vector2?](https://learn.microsoft.com/en-us/dotnet/api/System.Nullable-1?view=net-7.0) \

#### PlayerOffsetFromTarget

```csharp
public readonly Vector2? PlayerOffsetFromTarget;
```

Optional offset between the player entity and its camera follow target at the moment the transition began, preserved for the same reason as `PlayerOffsetFromCamera`.

**Returns** \
[Vector2?](https://learn.microsoft.com/en-us/dotnet/api/System.Nullable-1?view=net-7.0) \

⚡
