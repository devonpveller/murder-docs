# MurderInputAxis

**Namespace:** Murder.Core.Input \
**Assembly:** Murder.dll

```csharp
public class MurderInputAxis
```

Base class for input axis constants, numbers from 100 to 120 are reserved for the engine.
We recomend that if you need to create new constants for more gameplay axis, start at 0.

**Intent:** Defines the built-in logical input axis action IDs reserved by the engine.

**Use-case:** Refer to these constants when registering physical input bindings with `PlayerInput`; reserve IDs below 100 for game-specific axes.

### ⭐ Constructors

```csharp
public MurderInputAxis()
```

### ⭐ Properties

#### EditorCamera

```csharp
public static const int EditorCamera;
```

Axis id used exclusively by the Murder editor (not the runtime engine) to pan the scene camera. `Architect.Initialize()` registers it against the left/right gamepad thumbsticks and WASD-style keys, and `EditorCameraControllerSystem` reads it every frame to move the camera hook. Game code that only runs outside the editor will never see this axis updated — it exists purely so editor tooling has a dedicated, non-conflicting id in the engine-reserved range.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### Movement

```csharp
public static const int Movement;
```

Reserved axis id intended for player/entity movement. Unlike `Ui`, the engine does not register any bindings for it automatically — a game must call `Game.Input.RegisterAxes(MurderInputAxis.Movement, ...)` (or `Register(...)` with `InputButtonAxis` bindings) during its own startup, typically bound to WASD/arrow keys and a gamepad stick, and then read it each frame with `Game.Input.GetAxis(MurderInputAxis.Movement)` to drive character movement systems.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### Ui

```csharp
public static const int Ui;
```

Axis id for navigating menus/UI. This is one of the few axes the engine wires up itself: `Game.Initialize()` registers it to the left thumbstick, right thumbstick and D-pad, and `PlayerInput.VerticalMenu`, `HorizontalMenu` and `GridMenu` all read it internally to move the selection in a `MenuInfo`. If you want keyboard-driven menu navigation you should additionally bind arrow keys/WASD to this same id in your game's initialization code.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### UiTab

```csharp
public static const int UiTab;
```

Reserved axis id intended for switching between tabs in a tabbed UI panel. Unlike `Ui`, nothing in the engine registers or reads this axis automatically — it is simply carved out of the engine-reserved id range (100-120) so a game or the editor can bind and consume it directly without colliding with other built-in axes.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

⚡
