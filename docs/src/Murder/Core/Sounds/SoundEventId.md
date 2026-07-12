# SoundEventId

**Namespace:** Murder.Core.Sounds \
**Assembly:** Murder.dll

```csharp
[StructLayout(LayoutKind.Sequential)]
public sealed struct SoundEventId : IEqualityComparer<T>, IEquatable<T>
```

Identifies a sound event by the four 32-bit words of its FMOD event GUID, plus an optional `Path` string used only for display/tooling. Equality (`Equals`/`GetHashCode`) is based purely on the GUID words, so two `SoundEventId` values with different `Path`s but the same GUID compare as equal.

**Intent:** Reference a specific sound event for playback, stopping, or parameter control without depending on any particular audio middleware's own id type.

**Use-case:** Obtain a `SoundEventId` from an asset field picked in the editor (backed by the FMOD event browser) and pass it to `SoundServices.Play`, `ISoundPlayer.Stop`, or `ISoundPlayer.SetParameter` to drive audio at runtime. `SoundEventId.IsGuidEmpty` is checked by `SoundServices` before doing any work, so an unassigned field safely no-ops instead of throwing.

**Implements:** _[IEqualityComparer\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Generic.IEqualityComparer-1?view=net-7.0), [IEquatable\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.IEquatable-1?view=net-7.0)_

### ⭐ Properties

#### Data1

```csharp
public int Data1 { get; init; }
```

First 32-bit component of the FMOD event GUID.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### Data2

```csharp
public int Data2 { get; init; }
```

Second 32-bit component of the FMOD event GUID.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### Data3

```csharp
public int Data3 { get; init; }
```

Third 32-bit component of the FMOD event GUID.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### Data4

```csharp
public int Data4 { get; init; }
```

Fourth 32-bit component of the FMOD event GUID.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### EditorName

```csharp
public readonly string EditorName { get; }
```

Human-readable display name shown in the editor: the part of `Path` after its first `/` (e.g. `event:/Music/MainTheme` becomes `Music/MainTheme`), or the localized placeholder "Event path not found" if `Path` is `null`.

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### IsGuidEmpty

```csharp
public bool IsGuidEmpty { get; }
```

Returns `true` when all four data fields are zero (no event assigned). `SoundServices` checks this before issuing any play/update/stop call so an unset `SoundEventId` field is always a safe no-op.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### Path

```csharp
public readonly string? Path { get; init; }
```

The FMOD event path string (e.g. `event:/Music/MainTheme`).

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

### ⭐ Methods

#### WithPath(string)

```csharp
public SoundEventId WithPath(string path)
```

Returns a copy of this `SoundEventId` with `Path` set to `path`.

**Parameters** \
`path` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

**Returns** \
[SoundEventId](../../../Murder/Core/Sounds/SoundEventId.html) \

#### Equals(SoundEventId)

```csharp
public virtual bool Equals(SoundEventId other)
```

**Parameters** \
`other` [SoundEventId](../../../Murder/Core/Sounds/SoundEventId.html) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### Equals(SoundEventId, SoundEventId)

```csharp
public virtual bool Equals(SoundEventId x, SoundEventId y)
```

**Parameters** \
`x` [SoundEventId](../../../Murder/Core/Sounds/SoundEventId.html) \
`y` [SoundEventId](../../../Murder/Core/Sounds/SoundEventId.html) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### GetHashCode(SoundEventId)

```csharp
public virtual int GetHashCode(SoundEventId obj)
```

**Parameters** \
`obj` [SoundEventId](../../../Murder/Core/Sounds/SoundEventId.html) \

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

⚡
