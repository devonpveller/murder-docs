# InputState

**Namespace:** Murder.Core.Input \
**Assembly:** Murder.dll

```csharp
public sealed struct InputState
```

A snapshot of all raw input device states for a single frame.

**Intent:** Bundle keyboard, gamepad, and mouse state together for uniform processing by `VirtualButton` and `VirtualAxis`.

**Use-case:** `PlayerInput` constructs an `InputState` each frame and passes it to `IVirtualInput.Update()`. You typically do not need to create `InputState` directly.

### ⭐ Constructors
```csharp
public InputState(KeyboardState keyboardState, GamePadState gamePadState, MouseState mouseState)
```

**Parameters** \
`keyboardState` [KeyboardState](https://docs.monogame.net/api/Microsoft.Xna.Framework.Input.KeyboardState.html) \
`gamePadState` [GamePadState](https://docs.monogame.net/api/Microsoft.Xna.Framework.Input.GamePadState.html) \
`mouseState` [MouseState](https://docs.monogame.net/api/Microsoft.Xna.Framework.Input.MouseState.html) \

### ⭐ Properties
#### GamePadState
```csharp
public readonly GamePadState GamePadState;
```

The raw gamepad state captured this frame.

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

The raw mouse state captured this frame.

**Returns** \
[MouseState](https://docs.monogame.net/api/Microsoft.Xna.Framework.Input.MouseState.html) \


⚡