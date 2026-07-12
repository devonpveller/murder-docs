# IVirtualInput

**Namespace:** Murder.Core.Input \
**Assembly:** Murder.dll

```csharp
internal abstract IVirtualInput
```

Common contract implemented by `VirtualButton` and `VirtualAxis` so that `PlayerInput` can advance every registered virtual input uniformly, once per frame, without knowing whether it is polling a button or an axis.

**Intent:** Provide a single per-frame update entry point shared by all virtual input objects.

**Use-case:** This is an internal engine interface — game code does not implement it directly. `VirtualButton` and `VirtualAxis` implement it so `PlayerInput.Update()` can loop over its registered buttons and axes polymorphically and call `Update(InputState)` on each.

### ⭐ Methods

#### Update(InputState)

```csharp
public abstract void Update(InputState inputState)
```

Re-evaluates this virtual input's state (pressed/down/value/etc.) against the raw device snapshot captured this frame. Called by `PlayerInput.Update()` for every registered button and axis.

**Parameters** \
`inputState` [InputState](../../../Murder/Core/Input/InputState.html) \
The raw keyboard/mouse/gamepad state captured this frame. \

⚡
