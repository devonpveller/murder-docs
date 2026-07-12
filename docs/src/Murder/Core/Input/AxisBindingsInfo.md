# AxisBindingsInfo

**Namespace:** Murder.Core.Input \
**Assembly:** Murder.dll

```csharp
public sealed struct AxisBindingsInfo
```

A serializable snapshot of every `InputButtonAxis` binding currently registered on a `VirtualAxis`, keyed by the logical axis id it belongs to.

**Intent:** Persist the player's current (possibly rebound) axis bindings to disk/save data and later reconstruct an equivalent `VirtualAxis` — the plain `VirtualAxis` class itself is not meant to be serialized directly since it also carries runtime-only frame state.

**Use-case:** Build one with `new AxisBindingsInfo(key, virtualAxis)` when saving a rebinding profile, store the resulting `Buttons` array, and call `CreateVirtualAxis()` on load to rebuild a `VirtualAxis` with the same bindings — or pass it to `VirtualAxis`'s internal `Register(AxisBindingsInfo)` to merge it into an existing axis.

### ⭐ Constructors

```csharp
public AxisBindingsInfo(int key, VirtualAxis virtualAxis)
```

Captures a snapshot of every binding currently registered on `virtualAxis`, tagged with the logical axis id `key`.

**Parameters** \
`key` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
The logical axis id this snapshot is being recorded for. \
`virtualAxis` [VirtualAxis](../../../Murder/Core/Input/VirtualAxis.html) \
The live axis whose current bindings should be captured. \

### ⭐ Properties

#### Buttons

```csharp
public readonly ImmutableArray<InputButtonAxis> Buttons;
```

The set of directional/analog bindings captured from the source `VirtualAxis` at the time this snapshot was taken.

**Returns** \
[ImmutableArray\<InputButtonAxis\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \

#### Key

```csharp
public readonly int Key;
```

The logical axis id (matching a value passed to `PlayerInput.Register(int, InputButtonAxis[])`) that these bindings belong to.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

### ⭐ Methods

#### CreateVirtualAxis()

```csharp
public VirtualAxis CreateVirtualAxis()
```

Builds a new `VirtualAxis` and registers this snapshot's bindings onto it, effectively restoring a saved axis configuration.

**Returns** \
[VirtualAxis](../../../Murder/Core/Input/VirtualAxis.html) \
A freshly-created `VirtualAxis` carrying the same bindings recorded in this snapshot. \

⚡
