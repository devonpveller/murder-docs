# PackedSoundData

**Namespace:** Murder.Data \
**Assembly:** Murder.dll

```csharp
public class PackedSoundData
```

This has the data regarding all the sounds that will be loaded in the game.

**Intent:** Packages the sound asset manifest mapping FMOD event names to audio bank references.

**Use-case:** Loaded by the sound system at startup to resolve sound event IDs to the correct FMOD banks for the current platform.

### ⭐ Constructors
```csharp
public PackedSoundData()
```

### ⭐ Properties
#### Banks
```csharp
public ImmutableDictionary<TKey, TValue> Banks { get; public set; }
```

This has all the banks used by the sound engine, sorted by the supported platform, e.g. "Desktop".

**Returns** \
[ImmutableDictionary\<TKey, TValue\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableDictionary-2?view=net-7.0) \
#### Name
```csharp
public static const string Name;
```
Filename used when writing or reading the packed sound archive (always `sounds.gz`).

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
#### Plugins
```csharp
public ImmutableArray<T> Plugins { get; public set; }
```
List of sound-engine plugin filenames required at runtime (e.g. FMOD bank plugins).

**Returns** \
[ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \


⚡