# ParameterId

**Namespace:** Murder.Core.Sounds \
**Assembly:** Murder.dll

```csharp
[StructLayout(LayoutKind.Sequential)]
public sealed struct ParameterId : IEqualityComparer<T>, IEquatable<T>
```

Identifies an FMOD audio parameter by the two 32-bit words of its GUID, plus an optional `Name` and an `IsGlobal`/`Owner` pair that record whether the parameter is global or scoped to one specific event instance. Equality (`Equals`/`GetHashCode`) is based purely on the GUID words.

**Intent:** Reference a specific audio parameter for setting or querying via the sound system.

**Use-case:** Obtain a `ParameterId` from an asset field picked in the editor (backed by the FMOD parameter browser) and pass it to `ISoundPlayer.SetParameter`/`SetGlobalParameter`/`GetGlobalParameter` — or the higher-level `SoundServices.SetParameter`/`SetGlobalParameter`/`GetGlobalParameter` — to drive adaptive audio at runtime. `SoundRuleAction`/`ParameterRuleAction`-driven interactions such as `SetSoundParameterOnInteraction` use `ParameterId` to know which FMOD parameter to write to.

**Implements:** _[IEqualityComparer\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Generic.IEqualityComparer-1?view=net-7.0), [IEquatable\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.IEquatable-1?view=net-7.0)_

### ⭐ Constructors

```csharp
public ParameterId()
```

### ⭐ Properties

#### Data1

```csharp
public uint Data1 { get; init; }
```

First 32-bit component of the FMOD parameter GUID.

**Returns** \
[uint](https://learn.microsoft.com/en-us/dotnet/api/System.UInt32?view=net-7.0) \

#### Data2

```csharp
public uint Data2 { get; init; }
```

Second 32-bit component of the FMOD parameter GUID.

**Returns** \
[uint](https://learn.microsoft.com/en-us/dotnet/api/System.UInt32?view=net-7.0) \

#### EditorName

```csharp
public readonly string EditorName { get; }
```

Human-readable display name shown in the editor: empty string if `Name` is `null`, otherwise `Name` as-is when `IsGlobal` is `true`, or `"{Name} (local)"` when the parameter is scoped to a specific event instance.

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### IsGlobal

```csharp
public bool IsGlobal { get; init; }
```

`true` (the default) if this parameter is a global FMOD parameter; `false` if it is scoped to a specific event instance, in which case `Owner` identifies that instance.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### IsGuidEmpty

```csharp
public bool IsGuidEmpty { get; }
```

Returns `true` when both `Data1` and `Data2` are zero (no parameter assigned).

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### Name

```csharp
public readonly string? Name { get; init; }
```

Optional string name of the parameter as defined in the audio project.

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### Owner

```csharp
public SoundEventId? Owner { get; init; }
```

The `SoundEventId` that owns this parameter when it is a local (non-global) parameter, i.e. `IsGlobal` is `false`. Left `null` for global parameters.

**Returns** \
[SoundEventId?](../../../Murder/Core/Sounds/SoundEventId.html) \

### ⭐ Methods

#### WithPath(string)

```csharp
public ParameterId WithPath(string path)
```

Returns a copy of this `ParameterId` with `Name` set to `path`.

**Parameters** \
`path` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

**Returns** \
[ParameterId](../../../Murder/Core/Sounds/ParameterId.html) \

#### Equals(ParameterId)

```csharp
public virtual bool Equals(ParameterId other)
```

**Parameters** \
`other` [ParameterId](../../../Murder/Core/Sounds/ParameterId.html) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### Equals(ParameterId, ParameterId)

```csharp
public virtual bool Equals(ParameterId x, ParameterId y)
```

**Parameters** \
`x` [ParameterId](../../../Murder/Core/Sounds/ParameterId.html) \
`y` [ParameterId](../../../Murder/Core/Sounds/ParameterId.html) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### GetHashCode(ParameterId)

```csharp
public virtual int GetHashCode(ParameterId obj)
```

**Parameters** \
`obj` [ParameterId](../../../Murder/Core/Sounds/ParameterId.html) \

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

⚡
