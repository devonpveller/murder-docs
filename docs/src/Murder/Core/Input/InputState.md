# InputState

**Namespace:** Murder.Core.Input \
**Assembly:** Murder.dll

```csharp
public sealed struct InputState
```

An immutable snapshot of every raw input device's state for a single frame.

**Intent:** Bundle keyboard, gamepad, and mouse state together so every input query in a frame observes the exact same underlying device reads, instead of each caller re-polling FNA separately.

**Use-case:** `PlayerInput` builds one `InputState` each frame and passes it down to every registered `VirtualButton` and `VirtualAxis` via `IVirtualInput.Update`, and to `InputButton.Check`/`InputButtonAxis.Check`. You typically do not need to create an `InputState` directly.

### ⭐ Constructors

```csharp
public InputState(KeyboardState keyboardState, GamePadState gamePadState, MouseState mouseState)
```

Bundles the three raw device states captured for this frame into a single immutable snapshot.

**Parameters** \
`keyboardState` [KeyboardState](https://docs.monogame.net/api/Microsoft.Xna.Framework.Input.KeyboardState.html) \
`gamePadState` [GamePadState](https://docs.monogame.net/api/Microsoft.Xna.Framework.Input.GamePadState.html) \
`mouseState` [MouseState](https://docs.monogame.net/api/Microsoft.Xna.Framework.Input.MouseState.html) \

### ⭐ Properties

#### GamePadState

```csharp
public readonly GamePadState GamePadState;
```

The raw gamepad state (buttons, thumbsticks, triggers, connection status) captured this frame.

**Returns** \
[GamePadState](https://docs.monogame.net/api/Microsoft.Xna.Framework.Input.GamePadState.html) \

#### KeyboardState

```csharp
public readonly KeyboardState KeyboardState;
```

The raw keyboard state captured this frame.

**Returns** \
[KeyboardState](https://docs.monogame.net/api/Microsoft.Xna.Framework.Input.KeyboardState.html) \

#### MouseState

```csharp
public readonly MouseState MouseState;
```

The raw mouse state (position, buttons, scroll wheel) captured this frame.

**Returns** \
[MouseState](https://docs.monogame.net/api/Microsoft.Xna.Framework.Input.MouseState.html) \

⚡
