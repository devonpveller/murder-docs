# ParameterId

**Namespace:** Murder.Core.Sounds \
**Assembly:** Murder.dll

```csharp
public sealed struct ParameterId : IEqualityComparer<T>, IEquatable<T>
```

Identifies an audio parameter by its binary GUID data and optional human-readable name, compatible with FMOD parameter IDs.

**Intent:** Reference a specific audio parameter for setting or querying via the sound system.

**Use-case:** Obtain a `ParameterId` from your audio tooling (e.g. FMOD) and pass it to `ISoundPlayer.SetParameter()` or `SetGlobalParameter()` to adjust adaptive audio parameters at runtime.

**Implements:** _[IEqualityComparer\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Generic.IEqualityComparer-1?view=net-7.0), [IEquatable\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.IEquatable-1?view=net-7.0)_

### ⭐ Constructors
```csharp
public ParameterId()
```

### ⭐ Properties
#### Data1
```csharp
public uint Data1 { get; public set; }
```

First 32-bit component of the FMOD parameter GUID.

**Returns** \
[uint](https://learn.microsoft.com/en-us/dotnet/api/System.UInt32?view=net-7.0) \
#### Data2
```csharp
public uint Data2 { get; public set; }
```

Second 32-bit component of the FMOD parameter GUID.

**Returns** \
[uint](https://learn.microsoft.com/en-us/dotnet/api/System.UInt32?view=net-7.0) \
#### EditorName
```csharp
public string EditorName { get; }
```

Human-readable display name shown in the editor; appends "(local)" for non-global parameters.

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
#### IsGlobal
```csharp
public bool IsGlobal { get; public set; }
```

`true` if this parameter is a global FMOD parameter; `false` if it is scoped to a specific event instance.

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
public string Name { get; public set; }
```

Optional string name of the parameter as defined in the audio project.

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
#### Owner
```csharp
public T? Owner { get; public set; }
```

The `SoundEventId` that owns this parameter when it is a local (non-global) parameter.

**Returns** \
[T?](https://learn.microsoft.com/en-us/dotnet/api/System.Nullable-1?view=net-7.0) \
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