# PlayerInput

**Namespace:** Murder.Core.Input \
**Assembly:** Murder.dll

```csharp
public class PlayerInput
```

The central input manager that tracks button and axis state for keyboard, mouse, and gamepad each frame, and drives the built-in `MenuInfo`/`GenericMenuInfo<T>` navigation helpers.

**Intent:** Provide a single, game-accessible object for registering logical button/axis bindings, querying their per-frame state, persisting/restoring rebinding profiles, and advancing menu selection.

**Use-case:** Access `Game.Input` (a `PlayerInput` instance) in any system or service. Call `RegisterButton()`/`Register()`/`RegisterAxes()` at startup to bind physical keys/gamepad buttons/mouse buttons to logical int ids (see `MurderInputButtons`/`MurderInputAxis` for the engine's reserved ids), then call `Pressed()`, `Down()`, `GetAxis()`, and `VerticalMenu()`/`HorizontalMenu()`/`GridMenu()` each frame to drive gameplay and UI. `Game.Update()` calls `Update()` once per frame automatically; game code should never need to call it directly.

### ⭐ Constructors

```csharp
public PlayerInput()
```

### ⭐ Properties

#### AllAxis

```csharp
public Int32[] AllAxis { get; }
```

All registered axis IDs (debug only).

**Returns** \
[int[]](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### AllButtons

```csharp
public Int32[] AllButtons { get; }
```

All registered button IDs (debug only).

**Returns** \
[int[]](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### ControlChange

```csharp
public float ControlChange;
```

Unscaled timestamp of the most recent switch between keyboard/mouse and gamepad input (updated whenever `UsingKeyboard` flips inside `Update()`). UI code can use this to, for example, delay redrawing input prompts until the player has settled on one device for a moment.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### CurrentKeyboardState

```csharp
public KeyboardState CurrentKeyboardState { get; }
```

The raw MonoGame `KeyboardState` captured this frame — empty whenever `KeyboardConsumed` is `true` (e.g. an ImGui text field has focus) so game systems reading it directly don't also react to typing. Prefer the higher-level `Down(Keys)`/`Pressed(Keys)`/registered-button APIs over reading this directly unless you specifically need the raw frame snapshot.

**Returns** \
[KeyboardState](https://docs.monogame.net/api/Microsoft.Xna.Framework.Input.KeyboardState.html) \

#### CursorPosition

```csharp
public Point CursorPosition;
```

The mouse cursor's screen position, in pixels. Updated every frame from the raw device state regardless of `MouseConsumed` — the position itself is always current, only click/press queries are actually gated by consumption.

**Returns** \
[Point](../../../Murder/Core/Geometry/Point.html) \

#### KeyboardConsumed

```csharp
public bool KeyboardConsumed;
```

Keyboard ignored because the player is probably typing something on ImGui

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### MouseConsumed

```csharp
public bool MouseConsumed;
```

When `true`, mouse input is suppressed for this frame (e.g., an ImGui window has focus/hover) — `Update()` feeds an empty `MouseState` to every registered button/axis so gameplay doesn't react to clicks meant for editor UI. `CursorPosition` is still updated regardless, since knowing where the cursor is doesn't interfere with ImGui.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### ScrollWheel

```csharp
public int ScrollWheel { get; }
```

Scrollwheel delta

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### UsingKeyboard

```csharp
public bool UsingKeyboard;
```

If true player is using the keyboard, false means the player is using a game controller

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

### ⭐ Methods

#### Down(Buttons)

```csharp
public bool Down(Buttons button)
```

Returns `true` if the raw gamepad `button` is currently held on player one's controller, bypassing the virtual-button/registration system entirely. Rarely needed by gameplay code (prefer registering a logical button id and calling `Down(int)`); mainly useful for rebinding UI that needs to detect "which physical button did the player just press" without it being tied to an existing binding.

**Parameters** \
`button` [Buttons](https://docs.monogame.net/api/Microsoft.Xna.Framework.Input.Buttons.html) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### Down(int, bool)

```csharp
public bool Down(int button, bool raw = false)
```

Returns `true` if the virtual button `button` is currently held. When `raw` is `true`, ignores the consumed flag; if `button` was never registered, logs an error and returns `false`.

**Parameters** \
`button` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`raw` [bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### Down(Keys)

```csharp
public bool Down(Keys key)
```

Returns `true` if `key` is currently held, reading the live MonoGame keyboard state directly (not gated by `KeyboardConsumed`). Prefer registering a logical button id and calling `Down(int)` for gameplay; this raw overload is mainly useful for editor/tooling code that needs to react to a specific key regardless of registration.

**Parameters** \
`key` [Keys](https://docs.monogame.net/api/Microsoft.Xna.Framework.Input.Keys.html) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### GridMenu(GenericMenuInfo`1&, int, int, GridMenuFlags)

```csharp
public bool GridMenu(GenericMenuInfo`1& currentInfo, int width, int size, GridMenuFlags gridMenuFlags)
```

Advances a typed grid menu by one frame and returns `true` if the submit button was pressed.

**Parameters** \
`currentInfo` [GenericMenuInfo\<T\>&](../../../Murder/Core/Input/GenericMenuInfo-1.html) \
`width` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`size` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`gridMenuFlags` [GridMenuFlags](../../../Murder/Core/Input/GridMenuFlags.html) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### GridMenu(MenuInfo&, int, int, int, GridMenuFlags)

```csharp
public bool GridMenu(MenuInfo& currentInfo, int width, int maxHeight, int size, GridMenuFlags gridMenuFlags)
```

Advances a `MenuInfo` laid out as a 2D grid of `width` columns by one frame: reads the `Ui` axis to move the cursor horizontally/vertically (via `MenuInfo.NextAvailableOptionHorizontal`/`NextAvailableOptionVertical`), updates `Scroll` so the selection stays within `maxHeight` visible rows, and returns `true` if the submit button was pressed this frame (also updating `Canceled`/`OverflowX`/`OverflowY`). Set `gridMenuFlags` to control edge clamping/wrapping and diagonal rotation.

**Parameters** \
`currentInfo` [MenuInfo&](../../../Murder/Core/Input/MenuInfo.html) \
`width` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
Number of columns in the grid. \
`maxHeight` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
Number of rows visible at once before the grid scrolls. \
`size` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
Total number of options laid out in the grid. \
`gridMenuFlags` [GridMenuFlags](../../../Murder/Core/Input/GridMenuFlags.html) \
Edge-clamping/rotation behaviour; defaults to `GridMenuFlags.None`.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### HorizontalMenu(Int32&, int)

```csharp
public bool HorizontalMenu(Int32& selectedOption, int length)
```

Navigates a simple horizontal list of `length` items and returns `true` if submit was pressed. This is the lightest-weight menu helper — it takes a bare `int` selection instead of a `MenuInfo`/`GenericMenuInfo<T>`, so there is no scrolling, disabled-option support, or sound feedback; use it for very small, always-fully-enabled option lists (e.g. a 2-3 item toggle row).

**Parameters** \
`selectedOption` [int&](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`length` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### HorizontalMenu(MenuInfo&, SimpleMenuFlags)

```csharp
public bool HorizontalMenu(MenuInfo& currentInfo, SimpleMenuFlags flags)
```

Advances a `MenuInfo` by one frame, treating the `Ui` axis's horizontal component as the navigation direction (vertical input is reported back via `currentInfo.OverflowY` instead of moving the selection), and returns `true` if the submit button was pressed. Use this for menus laid out as a single horizontal row of options; pass `SimpleMenuFlags.Clamp` to stop at the ends instead of wrapping around.

**Parameters** \
`currentInfo` [MenuInfo&](../../../Murder/Core/Input/MenuInfo.html) \
`flags` [SimpleMenuFlags](../../../Murder/Core/Input/PlayerInput.html) \
Clamp behaviour at the menu's ends; defaults to `SimpleMenuFlags.None` (wrap around).

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### Pressed(int, bool)

```csharp
public bool Pressed(int button, bool raw = false)
```

Returns `true` if the virtual button `button` was just pressed this frame. When `raw` is `true`, ignores the consumed flag; if `button` was never registered, logs an error and returns `false`.

**Parameters** \
`button` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`raw` [bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### Pressed(Keys)

```csharp
public bool Pressed(Keys key)
```

Returns `true` if `key` was just pressed this frame, comparing the live keyboard state against last frame's snapshot directly (not gated by `KeyboardConsumed`).

**Parameters** \
`key` [Keys](https://docs.monogame.net/api/Microsoft.Xna.Framework.Input.Keys.html) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### PressedAndConsume(int)

```csharp
public bool PressedAndConsume(int button)
```

Returns `true` if `button` was just pressed, and immediately consumes it (and every other registered button sharing a physical binding) so subsequent reads return `false` this frame.

**Parameters** \
`button` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### Released(int)

```csharp
public bool Released(int button)
```

Returns `true` if the virtual button `button` was released this frame (was held last frame, not held now), reading the underlying `VirtualButton` directly without a `raw`/consumed-aware option.

**Parameters** \
`button` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### Released(Keys)

```csharp
public bool Released(Keys key)
```

Returns `true` if `key` was released this frame, comparing the live keyboard state against last frame's snapshot.

**Parameters** \
`key` [Keys](https://docs.monogame.net/api/Microsoft.Xna.Framework.Input.Keys.html) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### Shortcut(Chord)

```csharp
public bool Shortcut(Chord chord)
```

Returns `true` if `chord` (key + modifiers) was just activated this frame.

**Parameters** \
`chord` [Chord](../../../Murder/Core/Input/Chord.html) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### Shortcut(Keys, Keys[])

```csharp
public bool Shortcut(Keys key, Keys[] modifiers)
```

Returns `true` if `key` was just pressed while all `modifiers` are held, checking the raw (not `KeyboardConsumed`-gated) keyboard state. Returns `false` immediately if `key` is `Keys.None`. This is what editor keyboard shortcuts are typically built on, either directly or via the `Chord` overload.

**Parameters** \
`key` [Keys](https://docs.monogame.net/api/Microsoft.Xna.Framework.Input.Keys.html) \
`modifiers` [Keys[]](https://docs.monogame.net/api/Microsoft.Xna.Framework.Input.Keys.html) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### SimpleVerticalMenu(Int32&, int)

```csharp
public bool SimpleVerticalMenu(Int32& selectedOption, int length)
```

Navigates a simple vertical list of `length` items and returns `true` if submit was pressed. Like `HorizontalMenu(ref int, int)`, this is the bare-`int` variant with no scrolling/disabled-option/sound support — use it for small, always-enabled vertical option lists.

**Parameters** \
`selectedOption` [int&](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`length` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### VerticalMenu(GenericMenuInfo`1&)

```csharp
public bool VerticalMenu(GenericMenuInfo`1& currentInfo)
```

Advances a typed vertical menu by one frame and returns `true` if the submit button was pressed.

**Parameters** \
`currentInfo` [GenericMenuInfo\<T\>&](../../../Murder/Core/Input/GenericMenuInfo-1.html) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### VerticalMenu(MenuInfo&, SimpleMenuFlags)

```csharp
public bool VerticalMenu(MenuInfo& currentInfo, SimpleMenuFlags flags)
```

Advances a `MenuInfo` by one frame, treating the `Ui` axis's vertical component as the navigation direction (horizontal input is reported back via `currentInfo.OverflowX`), and returns `true` if the submit button was pressed. This is the most common menu helper — use it for standard top-to-bottom lists (pause menus, dialogs, inventory lists); pass `SimpleMenuFlags.Clamp` to stop at the ends instead of wrapping around.

**Parameters** \
`currentInfo` [MenuInfo&](../../../Murder/Core/Input/MenuInfo.html) \
`flags` [SimpleMenuFlags](../../../Murder/Core/Input/PlayerInput.html) \
Clamp behaviour at the menu's ends; defaults to `SimpleMenuFlags.None` (wrap around).

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### GetAnyGamepadButton()

```csharp
public Buttons? GetAnyGamepadButton()
```

Scans a fixed list of common gamepad buttons (D-pad, face buttons, shoulders/triggers, sticks, Start/Back) on player one's controller and returns the first one currently held, or `null` if none are (or no gamepad is connected). Used by input-remapping UI to detect "press any button to bind" without needing to register a `VirtualButton` first.

**Returns** \
[Buttons?](https://docs.monogame.net/api/Microsoft.Xna.Framework.Input.Buttons.html) \

#### GetAnyMouseButton()

```csharp
public MouseButtons? GetAnyMouseButton()
```

Returns the first pressed mouse button (`Left`, then `Middle`, then `Right`), or `null` if none are pressed or the game window is not the active application. Used by input-remapping UI for "click any mouse button to bind" flows.

**Returns** \
[MouseButtons?](../../../Murder/Core/Input/MouseButtons.html) \

#### GetAxisDescriptor(int)

```csharp
public string GetAxisDescriptor(int axis)
```

Returns a human-readable description of the bindings registered for axis `axis`.

**Parameters** \
`axis` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### GetButtonDescriptor(int)

```csharp
public string GetButtonDescriptor(int button)
```

Returns a human-readable description of the bindings registered for button `button`.

**Parameters** \
`button` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### GetKeyboardInput()

```csharp
public string GetKeyboardInput()
```

Returns the accumulated typed text from keyboard input since the last call to `ListenToKeyboardInput(true, ...)`/`SetKeyboardInput`. Only populated while raw text capture is active (see `ListenKeyboardHelper`).

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### GetAxis(int)

```csharp
public VirtualAxis GetAxis(int axis)
```

Returns the `VirtualAxis` registered under `axis`. Throws if `axis` was never registered — prefer `GetOrCreateAxis(int)` when you're not certain the axis has already been set up.

**Parameters** \
`axis` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

**Returns** \
[VirtualAxis](../../../Murder/Core/Input/VirtualAxis.html) \

#### GetOrCreateAxis(int)

```csharp
public VirtualAxis GetOrCreateAxis(int axis)
```

Returns an existing `VirtualAxis` for `axis`, or creates and registers a new (empty, unbound) one if it doesn't exist yet. This is what every `Register*`/`RegisterAxes*` overload calls internally before adding bindings, so it's always safe to call even before the axis has been set up.

**Parameters** \
`axis` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

**Returns** \
[VirtualAxis](../../../Murder/Core/Input/VirtualAxis.html) \

#### GetOrCreateButton(int)

```csharp
public VirtualButton GetOrCreateButton(int button)
```

Returns an existing `VirtualButton` for `button`, or creates and registers a new (empty, unbound) one if it doesn't exist yet. This is what every `RegisterButton`/`Register`/`Bind` overload calls internally before adding bindings, so it's always safe to call even before the button has been set up.

**Parameters** \
`button` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

**Returns** \
[VirtualButton](../../../Murder/Core/Input/VirtualButton.html) \

#### Bind(int, Action<InputState>)

```csharp
public void Bind(int button, Action<InputState> action)
```

Registers `action` to be called every time `button` transitions to pressed (subscribes to the underlying `VirtualButton.OnPress`). Use this for callback-driven input handling instead of polling `Pressed(int)` every frame; unregister everything bound to `button` with `ClearBinds(int)`.

**Parameters** \
`button` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`action` [Action\<InputState\>](https://learn.microsoft.com/en-us/dotnet/api/System.Action-1?view=net-7.0) \

#### ClampText(int)

```csharp
public void ClampText(int size)
```

Truncates the current keyboard text buffer to `size` characters.

**Parameters** \
`size` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### ClearAxis(int)

```csharp
public void ClearAxis(int id)
```

Removes every physical binding from the `VirtualAxis` registered under `id`, leaving it inert until re-registered. Used when rebuilding an axis's bindings from scratch (e.g. before applying a saved rebinding profile).

**Parameters** \
`id` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### ClearBinds(int)

```csharp
public void ClearBinds(int button)
```

Clears all binds from a button

**Parameters** \
`button` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### ClearBindsForButtonWith(int, Keys?, Buttons?)

```csharp
public void ClearBindsForButtonWith(int id, Nullable<Keys> key, Nullable<Buttons> button)
```

Removes only the specific keyboard `key` and/or gamepad `button` binding from the `VirtualButton` registered under `id`, leaving its other bindings intact. Used by rebinding UI to unbind a single physical input without wiping the whole logical button.

**Parameters** \
`id` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`key` [Keys?](https://docs.monogame.net/api/Microsoft.Xna.Framework.Input.Keys.html) \
`button` [Buttons?](https://docs.monogame.net/api/Microsoft.Xna.Framework.Input.Buttons.html) \

#### ClearButton(int)

```csharp
public void ClearButton(int id)
```

Clears every `OnPress` callback and every physical binding from the `VirtualButton` registered under `id`, fully resetting it to an empty, unbound state.

**Parameters** \
`id` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### Consume(int)

```csharp
public void Consume(int button)
```

Consumes all buttons that have anything in common with this

**Parameters** \
`button` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### ConsumeAll()

```csharp
public void ConsumeAll()
```

Marks all registered buttons and axes as consumed for the current frame.

#### DeregisterAll(int)

```csharp
public void DeregisterAll(int axis)
```

Removes every physical binding from the `VirtualAxis` registered under `axis`, leaving it inert until re-registered. (Despite the surrounding XML summary in the source referring to registration, this method deregisters — it is the axis counterpart of `VirtualButton.DeregisterAll()`.)

**Parameters** \
`axis` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### ListenToKeyboardInput(bool, int)

```csharp
public void ListenToKeyboardInput(bool enable, int maxCharacters = 32)
```

Enables or disables raw keyboard text capture, limiting input to `maxCharacters`. Prefer wrapping this in a `ListenKeyboardHelper` (`using` block) rather than calling it directly, so capture is reliably disabled again even if the caller exits early or throws.

**Parameters** \
`enable` [bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
`maxCharacters` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### LoadFromPreferences(GamePreferences)

```csharp
public void LoadFromPreferences(GamePreferences gamePreferences)
```

Rebuilds every button/axis registered in the game's `InputProfileAsset` from `gamePreferences`: for bindings the player is allowed to customize (`AllowPlayerCustomization`) and that have a saved snapshot in `gamePreferences.ButtonBindingsInfos`/`AxisBindingsInfos`, restores that saved snapshot; otherwise falls back to the profile's default bindings. Call this once at startup (after registering the `InputProfileAsset` in `GameProfile`) to apply the player's saved rebindings.

**Parameters** \
`gamePreferences` [GamePreferences](../../../Murder/Save/GamePreferences.html) \

#### LockInput(bool)

```csharp
public void LockInput(bool @lock)
```

When `@lock` is `true`, immediately feeds every registered button/axis an empty input state (via `UpdateOnEmpty()`) and then freezes all further input processing — `Update()` becomes a no-op until unlocked. When `false`, resumes normal per-frame updates. Use this to suppress all player input during a cutscene or scripted sequence without having to disable every individual system that reads it.

**Parameters** \
`@lock` [bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### MockInput(int)

```csharp
public void MockInput(int button)
```

Forces the `VirtualButton` registered under `button` to report as pressed this frame (via `VirtualButton.Press()`), bypassing the physical device entirely. Useful for automated tests, tutorials, or triggering a gameplay action from a non-input source (e.g. a UI button click that should also count as pressing the corresponding gameplay button).

**Parameters** \
`button` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### MockInput(int, Vector2)

```csharp
public void MockInput(int axis, Vector2 value)
```

Forces the `VirtualAxis` registered under `axis` to report `value` this frame (via `VirtualAxis.Press(Vector2)`), bypassing the physical device entirely. Useful for automated tests or driving menu/gameplay navigation from a non-stick input source (e.g. an on-screen virtual joystick).

**Parameters** \
`axis` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`value` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

#### MockNoInput()

```csharp
public void MockNoInput()
```

Feeds every registered button/axis a single empty input state for this frame (equivalent to `UpdateOnEmpty()`), without permanently locking future updates the way `LockInput(true)` does. Use this to simulate "no input this frame" once, e.g. while a modal dialog briefly steals focus.

#### Register(int, InputButtonAxis[])

```csharp
public void Register(int axis, InputButtonAxis[] buttonAxes)
```

Registers input axes

**Parameters** \
`axis` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`buttonAxes` [InputButtonAxis[]](../../../Murder/Core/Input/InputButtonAxis.html) \

#### Register(int, MouseButtons[])

```csharp
public void Register(int button, MouseButtons[] buttons)
```

Registers mouse buttons as bindings for virtual button `button`. Functionally identical to `RegisterButton(int, MouseButtons[])` below — the two overloads exist under different names but do exactly the same thing; either can be used interchangeably.

**Parameters** \
`button` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`buttons` [MouseButtons[]](../../../Murder/Core/Input/MouseButtons.html) \

#### RegisterAxes(int, GamepadAxis[])

```csharp
public void RegisterAxes(int axis, GamepadAxis[] gamepadAxis)
```

Registers a gamepad axis as a button

**Parameters** \
`axis` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`gamepadAxis` [GamepadAxis[]](../../../Murder/Core/Input/GamepadAxis.html) \

#### RegisterAxesAsButton(int, GamepadAxis[])

```csharp
public void RegisterAxesAsButton(int button, GamepadAxis[] gamepadAxis)
```

Registers a gamepad axis as a button

**Parameters** \
`button` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`gamepadAxis` [GamepadAxis[]](../../../Murder/Core/Input/GamepadAxis.html) \

#### RegisterButton(int, Buttons[])

```csharp
public void RegisterButton(int button, Buttons[] buttons)
```

Registers one or more gamepad buttons as bindings for virtual button `button`, skipping any that are already bound.

**Parameters** \
`button` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`buttons` [Buttons[]](https://docs.monogame.net/api/Microsoft.Xna.Framework.Input.Buttons.html) \

#### RegisterButton(int, Keys[])

```csharp
public void RegisterButton(int button, Keys[] keys)
```

Registers a keyboard key as a button

**Parameters** \
`button` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`keys` [Keys[]](https://docs.monogame.net/api/Microsoft.Xna.Framework.Input.Keys.html) \

#### RegisterButton(int, MouseButtons[])

```csharp
public void RegisterButton(int button, MouseButtons[] buttons)
```

Registers one or more mouse buttons as bindings for virtual button `button`. See `Register(int, MouseButtons[])` above — this overload is interchangeable with it.

**Parameters** \
`button` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`buttons` [MouseButtons[]](../../../Murder/Core/Input/MouseButtons.html) \

#### RegisterFlickerProtection(int, float)

```csharp
public void RegisterFlickerProtection(int button, float flickerProtection)
```

Set a minimum cooldown for input on this button.

**Parameters** \
`button` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`flickerProtection` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### RestoreAllDefaults()

```csharp
public void RestoreAllDefaults()
```

Resets every button registered in the game's `InputProfileAsset` back to its default bindings, clearing whatever the player had customized. Requires `GameProfile.InputProfile` to point at a valid `InputProfileAsset`; logs a warning and does nothing otherwise.

#### RestoreAxisDefaults(int)

```csharp
public void RestoreAxisDefaults(int id)
```

Resets the single axis `id` back to its default bindings as defined in the game's `InputProfileAsset`, discarding any custom bindings for that axis only.

**Parameters** \
`id` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### RestoreDefaults(int)

```csharp
public void RestoreDefaults(int id)
```

Resets the single button `id` back to its default bindings as defined in the game's `InputProfileAsset`, discarding any custom bindings for that button only.

**Parameters** \
`id` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### SaveCurrentToPreferences(GamePreferences)

```csharp
public void SaveCurrentToPreferences(GamePreferences gamePreferences)
```

Snapshots the current bindings of every registered button into a `ButtonBindingsInfo` array and stores them on `gamePreferences` via `SetButtonBindingsInfos`. Call this after the player finishes rebinding controls so the changes persist to save data; pair with `LoadFromPreferences(GamePreferences)` to restore them on the next launch.

**Parameters** \
`gamePreferences` [GamePreferences](../../../Murder/Save/GamePreferences.html) \

#### SetKeyboardInput(string)

```csharp
public void SetKeyboardInput(string value)
```

Overwrites the captured keyboard text buffer with `value`, replacing whatever the player had typed so far. Useful for pre-filling a text field (e.g. showing an existing save name before the player edits it) while keyboard capture is active.

**Parameters** \
`value` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### Update()

```csharp
public void Update()
```

Pulls new device state each frame and updates all registered buttons and axes.

#### UpdateOnEmpty()

```csharp
public void UpdateOnEmpty()
```

Feeds every registered button and axis a single empty `InputState` (no keys, no gamepad, no mouse), causing all of them to report not-pressed/not-down for this frame without touching `CursorPosition` or any other unrelated state. Backing implementation for `LockInput(true)` and `MockNoInput()`.

⚡
