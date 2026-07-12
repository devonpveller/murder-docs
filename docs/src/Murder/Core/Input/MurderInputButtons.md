# MurderInputButtons

**Namespace:** Murder.Core.Input \
**Assembly:** Murder.dll

```csharp
public class MurderInputButtons
```

Base class for input button constants, numbers from 100 to 120 are reserved for the engine.
We recomend that if you need to create new constants for more gameplay buttons, start at 0.

**Intent:** Defines the built-in logical input button action IDs reserved by the engine.

**Use-case:** Refer to these constants when registering physical input bindings with `PlayerInput`; reserve IDs below 100 for game-specific buttons.

### ⭐ Constructors

```csharp
public MurderInputButtons()
```

### ⭐ Properties

#### Backspace

```csharp
public static const int Backspace;
```

Button id intended for the Backspace key, auto-registered to `Keys.Back` and `Keys.BrowserBack` by the engine (`Game.Initialize()`). See the note on `Space` below: this constant currently has the same numeric value (112) as `Space`, so the two ids are not distinguishable at runtime — both resolve to one shared `VirtualButton`.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### Cancel

```csharp
public static const int Cancel;
```

Button id for the cancel/back action. `PlayerInput.HorizontalOrVerticalMenu` and `GridMenu` check `Pressed(MurderInputButtons.Cancel)` every frame to set `MenuInfo.Canceled`, so any binding you register to this id (Escape key, gamepad B, etc.) drives "back out of this menu" behavior across every menu in the game.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### Ctrl

```csharp
public static const int Ctrl;
```

Button id for the Ctrl modifier key. Auto-registered by the engine (`Game.Initialize()`) to both the left and right Control keys, so editor/tooling shortcuts can check `Game.Input.Down(MurderInputButtons.Ctrl)` without caring which physical Ctrl key is held.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### Debug

```csharp
public static const int Debug;
```

Button id used for the engine's debug-mode toggle. Auto-registered to F1 in `Game.Initialize()`, and read internally to feed the debug button state to ImGui-driven tooling while the cursor is captured.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### Delete

```csharp
public static const int Delete;
```

Button id for the Delete key. Auto-registered by the engine (`Game.Initialize()`) so editor panels and asset browsers can bind delete-selection behavior to a single, well-known id.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### Esc

```csharp
public static const int Esc;
```

Button id for the Escape key. Auto-registered by the engine (`Game.Initialize()`) as a general-purpose "close/dismiss" input, independent of `Cancel` (which is intended for in-game menu navigation).

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### LeftClick

```csharp
public static const int LeftClick;
```

Button id for the left mouse button. Auto-registered by the engine (`Game.Initialize()`) via `RegisterButton(MurderInputButtons.LeftClick, MouseButtons.Left)`, so any system can query left-click state with `Game.Input.Pressed(MurderInputButtons.LeftClick)`/`Down(...)` without registering the binding itself. `PlayerInput.Update()` also special-cases this id (along with `RightClick`/`MiddleClick`) to avoid re-centering the cursor when only mouse-click buttons are bound.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### MiddleClick

```csharp
public static const int MiddleClick;
```

Button id for the middle mouse button. Auto-registered by the engine (`Game.Initialize()`) via `RegisterButton(MurderInputButtons.MiddleClick, MouseButtons.Middle)`; see `LeftClick` for how this id interacts with `PlayerInput.Update()`'s mouse-locking logic.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### Pause

```csharp
public static const int Pause;
```

Button id reserved for the pause action. Not registered or consumed anywhere in the engine itself — a game is expected to bind a physical key/button to it and check `Game.Input.Pressed(MurderInputButtons.Pause)` to toggle its own pause state.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### PlayGame

```csharp
public static const int PlayGame;
```

Button id for starting or resuming gameplay from the editor. Auto-registered to F5 in `Game.Initialize()`, matching the common "run" hotkey used by the Murder editor to enter play mode.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### RightClick

```csharp
public static const int RightClick;
```

Button id for the right mouse button. Auto-registered by the engine (`Game.Initialize()`) via `RegisterButton(MurderInputButtons.RightClick, MouseButtons.Right)`; see `LeftClick` for how this id interacts with `PlayerInput.Update()`'s mouse-locking logic.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### Shift

```csharp
public static const int Shift;
```

Button id for the Shift modifier key. Auto-registered by the engine (`Game.Initialize()`) to the left Shift key only (unlike `Ctrl`, which binds both left and right).

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### Space

```csharp
public static const int Space;
```

Button id for the Spacebar, auto-registered to `Keys.Space` by the engine (`Game.Initialize()`). **Note:** this constant shares its numeric value (112) with `Backspace` below. Because the engine registers bindings for both ids during startup, they resolve to the same underlying `VirtualButton` — in practice, checking either `Space` or `Backspace` reports the same combined state (Space, Back, and BrowserBack all pressed together). Treat them as aliases rather than independent buttons.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### Submit

```csharp
public static const int Submit;
```

Button id for the confirm/submit action (e.g. Enter, gamepad A). This is the id `PlayerInput.HorizontalOrVerticalMenu` and `GridMenu` check via `Pressed(MurderInputButtons.Submit)` to fire the "confirm this selection" return value from `VerticalMenu`, `HorizontalMenu` and `GridMenu`; a game must register its own physical bindings to it for menus to be usable.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

⚡
