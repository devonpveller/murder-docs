# VirtualButton

**Namespace:** Murder.Core.Input \
**Assembly:** Murder.dll

```csharp
public class VirtualButton : IVirtualInput
```

Runtime state container for a logical button input — tracks pressed/down/released state and held duration.

**Intent:** Maintain the per-frame state of a logical button mapped to one or more `InputButton` bindings.

**Use-case:** Access via `PlayerInput.GetOrCreateButton(int)`. Check `Pressed` for just-pressed (one frame), `Down` for held, and `Consumed` to gate input handling. Call `Consume()` to prevent other systems from reacting to the same press.

**Implements:** _[IVirtualInput](../../../Murder/Core/Input/IVirtualInput.html)_

### ⭐ Constructors
```csharp
public VirtualButton()
```

### ⭐ Properties
#### _lastPressedButton
```csharp
public Nullable`1[] _lastPressedButton;
```

Tracks the last pressed `InputButton` for keyboard (index 1) and gamepad (index 0).

**Returns** \
[T?[]](https://learn.microsoft.com/en-us/dotnet/api/System.Nullable-1?view=net-7.0) \
#### Buttons
```csharp
public List<T> Buttons;
```

The list of physical `InputButton` bindings registered to this virtual button.

**Returns** \
[List\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Generic.List-1?view=net-7.0) \
#### Consumed
```csharp
public bool Consumed;
```

When `true`, the button has been consumed this frame and `Pressed` returns `false`.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
#### Down
```csharp
public bool Down { get; private set; }
```

`true` while any bound physical button is held.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
#### LastPressed
```csharp
public float LastPressed;
```

Unscaled timestamp of the most recent press.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
#### LastReleased
```csharp
public float LastReleased;
```

Unscaled timestamp of the most recent release.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
#### Pressed
```csharp
public bool Pressed { get; }
```

`true` for the single frame when the button is first pressed (not held, not consumed).

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
#### Previous
```csharp
public bool Previous { get; private set; }
```

`true` if the button was held during the previous frame.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
### ⭐ Events
#### OnPress
```csharp
public event Action<T> OnPress;
```

Fired every frame the button is pressed (first frame only, before consume).

**Returns** \
[Action\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Action-1?view=net-7.0) \
### ⭐ Methods
#### LastPressedButton(bool)
```csharp
public InputButton LastPressedButton(bool keyboard)
```

Returns the last `InputButton` that was pressed, from keyboard/mouse (`keyboard=true`) or gamepad (`keyboard=false`).

**Parameters** \
`keyboard` [bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

**Returns** \
[InputButton](../../../Murder/Core/Input/InputButton.html) \

#### GetDescriptor()
```csharp
public string GetDescriptor()
```

Returns a human-readable description of the bindings registered to this button.

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### Update(InputState)
```csharp
public virtual void Update(InputState inputState)
```

**Parameters** \
`inputState` [InputState](../../../Murder/Core/Input/InputState.html) \

#### Consume()
```csharp
public void Consume()
```

Marks this button as consumed for the current frame, preventing further reads from seeing it as pressed.

#### Free()
```csharp
public void Free()
```

Clears the consumed flag, allowing the button to be read again this frame.



⚡