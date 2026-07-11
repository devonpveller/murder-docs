# SoundEventId

**Namespace:** Murder.Core.Sounds \
**Assembly:** Murder.dll

```csharp
public sealed struct SoundEventId : IEqualityComparer<T>, IEquatable<T>
```

Identifies a sound event by its 128-bit GUID data and optional path string, compatible with FMOD event GUIDs.

**Intent:** Reference a specific sound event for playback, stopping, or parameter control.

**Use-case:** Obtain a `SoundEventId` from the editor asset browser and pass it to `SoundServices.Play()`, `ISoundPlayer.Stop()`, or `ISoundPlayer.SetParameter()` to drive audio at runtime.

**Implements:** _[IEqualityComparer\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Generic.IEqualityComparer-1?view=net-7.0), [IEquatable\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.IEquatable-1?view=net-7.0)_

### ⭐ Properties
#### Data1
```csharp
public int Data1 { get; public set; }
```

First 32-bit component of the FMOD event GUID.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
#### Data2
```csharp
public int Data2 { get; public set; }
```

Second 32-bit component of the FMOD event GUID.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
#### Data3
```csharp
public int Data3 { get; public set; }
```

Third 32-bit component of the FMOD event GUID.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
#### Data4
```csharp
public int Data4 { get; public set; }
```

Fourth 32-bit component of the FMOD event GUID.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
#### EditorName
```csharp
public string EditorName { get; }
```

Human-readable display name shown in the editor, derived from the event `Path`.

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
#### IsGuidEmpty
```csharp
public bool IsGuidEmpty { get; }
```

Returns `true` when all four data fields are zero (no event assigned).

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
#### Path
```csharp
public string Path { get; public set; }
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