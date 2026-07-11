# IVirtualInput

**Namespace:** Murder.Core.Input \
**Assembly:** Murder.dll

```csharp
abstract IVirtualInput
```

Internal interface implemented by `VirtualButton` and `VirtualAxis` for uniform per-frame input polling.

**Intent:** Provide a common contract for all virtual input objects so `PlayerInput` can update them uniformly.

**Use-case:** You do not implement this interface directly; `VirtualButton` and `VirtualAxis` implement it internally.

### ⭐ Methods
#### Update(InputState)
```csharp
public abstract void Update(InputState inputState)
```

Updates the internal state of this virtual input from the raw `inputState` captured this frame.

**Parameters** \
`inputState` [InputState](../../../Murder/Core/Input/InputState.html) \



⚡