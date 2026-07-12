# ButtonBindingsInfo

**Namespace:** Murder.Core.Input \
**Assembly:** Murder.dll

```csharp
public sealed struct ButtonBindingsInfo
```

A serializable snapshot of every `InputButton` binding currently registered on a `VirtualButton`, keyed by the logical button id it belongs to.

**Intent:** Persist the player's current (possibly rebound) button bindings to disk/save data and later reconstruct an equivalent `VirtualButton` — the plain `VirtualButton` class itself is not meant to be serialized directly since it also carries runtime-only frame state.

**Use-case:** Build one with `new ButtonBindingsInfo(key, virtualButton)` when saving a rebinding profile, store the resulting `Buttons` array, and call `CreateVirtualButton()` on load to rebuild a `VirtualButton` with the same bindings — or pass it to `VirtualButton.Register(ButtonBindingsInfo)` to merge it into an existing button.

### ⭐ Constructors

```csharp
public ButtonBindingsInfo(int key, VirtualButton virtualButton)
```

Captures a snapshot of every binding currently registered on `virtualButton`, tagged with the logical button id `key`.

**Parameters** \
`key` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
The logical button id this snapshot is being recorded for. \
`virtualButton` [VirtualButton](../../../Murder/Core/Input/VirtualButton.html) \
The live button whose current bindings should be captured. \

### ⭐ Properties

#### Buttons

```csharp
public readonly ImmutableArray<InputButton> Buttons;
```

The set of bindings captured from the source `VirtualButton` at the time this snapshot was taken.

**Returns** \
[ImmutableArray\<InputButton\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \

#### Key

```csharp
public readonly int Key;
```

The logical button id (matching a value passed to `PlayerInput.Register(int, Keys[])` or a similar overload) that these bindings belong to.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

### ⭐ Methods

#### CreateVirtualButton()

```csharp
public VirtualButton CreateVirtualButton()
```

Builds a new `VirtualButton` and registers this snapshot's bindings onto it, effectively restoring a saved button configuration.

**Returns** \
[VirtualButton](../../../Murder/Core/Input/VirtualButton.html) \
A freshly-created `VirtualButton` carrying the same bindings recorded in this snapshot. \

⚡
