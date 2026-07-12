# VirtualButton

**Namespace:** Murder.Core.Input \
**Assembly:** Murder.dll

```csharp
public class VirtualButton : IVirtualInput
```

Runtime state container for a logical button input — tracks pressed/down/released state, held duration and the set of physical `InputButton` bindings (keyboard keys, gamepad buttons, mouse buttons or gamepad axes-as-buttons) mapped to it.

**Intent:** Maintain the per-frame state of a logical button mapped to one or more `InputButton` bindings, decoupling gameplay/UI code from the specific physical keys/buttons the player has bound.

**Use-case:** Access via `PlayerInput.GetOrCreateButton(int)`/`PlayerInput.GetAnyGamepadButton()`-style APIs, or indirectly through `Game.Input.Pressed(int)`/`Down(int)`/`Released(int)`. Check `Pressed` for just-pressed (one frame), `Down` for held, and `Consumed` to gate input handling. Call `Consume()` to prevent other systems from reacting to the same press (`PlayerInput.Consume(int)` also consumes every other registered button that shares a physical binding with this one).

**Implements:** _[IVirtualInput](../../../Murder/Core/Input/IVirtualInput.html)_

### ⭐ Constructors

```csharp
public VirtualButton()
```

Creates an empty button with no bindings; call `Register(...)` (directly or via `PlayerInput.RegisterButton`) to add keyboard/gamepad/mouse bindings before it can report any state.

### ⭐ Properties

#### \_lastPressedButton

```csharp
public InputButton?[] _lastPressedButton;
```

A 2-element array tracking the most recently pressed `InputButton` for keyboard/mouse input (index 1, when `Game.Input.UsingKeyboard` is `true`) and gamepad input (index 0). Backing store for `LastPressedButton(bool)`.

**Returns** \
[InputButton?[]](../../../Murder/Core/Input/InputButton.html) \

#### Buttons

```csharp
public ImmutableArray<InputButton> Buttons;
```

The set of physical `InputButton` bindings registered to this virtual button. Populated via the various `Register(...)` overloads; `Update(InputState)` checks each entry in order and stops at the first one that is currently active.

**Returns** \
[ImmutableArray\<InputButton\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \

#### Consumed

```csharp
public bool Consumed;
```

When `true`, the button has been consumed this frame and `Pressed` returns `false`. Cleared automatically at the start of the next `Update(InputState)` call once the button is no longer held.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### Down

```csharp
public bool Down { get; private set; }
```

`true` while any bound physical button is held, recomputed every `Update(InputState)` call. Unlike `Pressed`, this stays `true` across multiple frames while the button is held down and ignores `Consumed`.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### FlickerProtection

```csharp
public float FlickerProtection { get; private set; }
```

A minimum cooldown (in seconds) between registered presses, set via `SetFlickerProtection(float)`. If a new press happens within this window of the previous one, `Update(InputState)` forces `Down` back to `false` for that frame — useful for noisy/flaky physical inputs (e.g. a worn gamepad trigger) that can otherwise double-fire.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### HeldTime

```csharp
public float HeldTime;
```

Accumulated unscaled seconds the button has been continuously held; reset to `0` the frame it's released and every time it registers a fresh `Pressed`. Use this to implement charge-up mechanics or long-press gestures without tracking timestamps manually.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### LastPressed

```csharp
public float LastPressed;
```

Unscaled timestamp of the most recent press, updated both by `Update(InputState)` (on a real device press) and by `Press()` (a forced/mocked press).

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### LastReleased

```csharp
public float LastReleased;
```

Unscaled timestamp of the most recent release, updated by `Update(InputState)` when the button transitions from held to not-held.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### Pressed

```csharp
public bool Pressed { get; }
```

`true` for the single frame when the button is first pressed (down this frame, not down the previous frame, and not consumed). This is the property most gameplay/UI code should read for "was this button just pressed" logic — use `PlayerInput.Pressed(int)`/`PressedAndConsume(int)` rather than reaching into this directly when the button is managed by `PlayerInput`.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### Previous

```csharp
public bool Previous { get; private set; }
```

`true` if the button was held during the previous frame; used internally to derive `Pressed` and `Released`.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### UsingMouse

```csharp
public bool UsingMouse;
```

Whether we are using mouse as an input source for this button.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

### ⭐ Events

#### OnPress

```csharp
public event Action<InputState> OnPress;
```

Fired once during `Update(InputState)` on the frame the button transitions to `Pressed` (before flicker protection can suppress it on a later check). Register via `PlayerInput.Bind(int, Action<InputState>)` for callback-driven input handling instead of polling `Pressed` every frame; unregister everything at once with `ClearBinds()`/`PlayerInput.ClearBinds(int)`.

**Returns** \
[Action\<InputState\>](https://learn.microsoft.com/en-us/dotnet/api/System.Action-1?view=net-7.0) \

### ⭐ Methods

#### GetDescriptor()

```csharp
public string GetDescriptor()
```

Returns a human-readable, comma/or-joined description of the currently-connected-gamepad-compatible bindings on this button (e.g. `"A or Space"`), built from each binding's `ToString()`. Used by input-remapping/help UI to show the player what's currently bound.

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### LastPressedButton(bool)

```csharp
public InputButton LastPressedButton(bool keyboard)
```

Returns the last `InputButton` that was pressed, from keyboard/mouse (`keyboard=true`) or gamepad (`keyboard=false`). Falls back to the first registered binding matching that source (or the first binding overall) if nothing has been pressed yet. Used by input-prompt UI to show the correct icon/glyph for whichever device the player last used.

**Parameters** \
`keyboard` [bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

**Returns** \
[InputButton](../../../Murder/Core/Input/InputButton.html) \

#### Consume()

```csharp
public void Consume()
```

Marks this button as consumed for the current frame, preventing further reads of `Pressed` from seeing it as pressed. `PlayerInput.Consume(int)` calls this and also consumes every other registered `VirtualButton` that shares at least one physical `InputButton` binding, so that, e.g., pressing Space doesn't simultaneously trigger two different logical actions both bound to Space.

#### DeregisterAll()

```csharp
public void DeregisterAll()
```

Removes every physical binding from `Buttons` and clears `_lastPressedButton`, leaving the button with no way to be triggered until new bindings are registered. Used when rebuilding a button's bindings from scratch (e.g. loading a saved rebinding profile or restoring defaults).

#### Deregister(Keys?, Buttons?)

```csharp
public void Deregister(Nullable<Keys> key, Nullable<Buttons> button)
```

Removes any binding in `Buttons` whose keyboard key matches `key` or whose gamepad button matches `button` (pass `null` for whichever one you don't want to match on). Used by input-remapping UI to unbind a specific key/button before rebinding it to something else.

**Parameters** \
`key` [Keys?](https://docs.monogame.net/api/Microsoft.Xna.Framework.Input.Keys.html) \
`button` [Buttons?](https://docs.monogame.net/api/Microsoft.Xna.Framework.Input.Buttons.html) \

#### Free()

```csharp
public void Free()
```

Clears the consumed flag, allowing the button to be read again this frame. The inverse of `Consume()`.

#### Press()

```csharp
public void Press()
```

Force pressing the button, bypassing the physical device state entirely: sets `Down` to `true`, `Previous` to `false` and stamps `LastPressed` with the current time. This is what `PlayerInput.MockInput(int)` calls under the hood, useful for automated tests, tutorials/scripted sequences, or simulating a button press from an unrelated input source (e.g. a UI button click that should also count as pressing a gameplay action).

#### Register(ButtonBindingsInfo)

```csharp
public void Register(ButtonBindingsInfo bindingsInfo)
```

Adds every binding captured in `bindingsInfo.Buttons` to this button's `Buttons` array, without clearing existing bindings first. Used to restore a serialized `ButtonBindingsInfo` snapshot (e.g. loaded from save data / player preferences) onto a fresh or existing `VirtualButton`.

**Parameters** \
`bindingsInfo` [ButtonBindingsInfo](../../../Murder/Core/Input/ButtonBindingsInfo.html) \

#### SetFlickerProtection(float)

```csharp
public void SetFlickerProtection(float flickerProtection)
```

Sets `FlickerProtection`, the minimum cooldown (in seconds) enforced between presses. `PlayerInput.RegisterFlickerProtection(int, float)` is the usual entry point for this; call it for bindings prone to double-firing (e.g. certain gamepad triggers).

**Parameters** \
`flickerProtection` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### Update(InputState)

```csharp
public virtual void Update(InputState inputState)
```

Recomputes `Previous`, `Down`, `UsingMouse` and `HeldTime` from `inputState` against every registered `Buttons` entry, applies `FlickerProtection`, fires `OnPress` on a fresh press, and stamps `LastPressed`/`LastReleased`. Called once per frame by `PlayerInput.Update()` for every registered button; game code should not normally call this directly.

**Parameters** \
`inputState` [InputState](../../../Murder/Core/Input/InputState.html) \

⚡
