# WorldFlags

**Namespace:** Murder.Assets \
**Assembly:** Murder.dll

```csharp
public sealed enum WorldFlags : Enum, IComparable, ISpanFormattable, IFormattable, IConvertible
```

Per-world behavior flags authored on a `WorldAsset`.

**Intent:** Let a level designer opt an individual world out of default engine transition behavior (sound fading, save persistence) without writing code.

**Use-case:** Set `WorldAsset.Flags` in the editor. Only `NeverPersist` is currently read by the engine (checked by the save system to skip persisting a world's state); the sound-fade flags are reserved for game-specific code that wants to react to them.

**Implements:** _[Enum](https://learn.microsoft.com/en-us/dotnet/api/System.Enum?view=net-7.0), [IComparable](https://learn.microsoft.com/en-us/dotnet/api/System.IComparable?view=net-7.0), [ISpanFormattable](https://learn.microsoft.com/en-us/dotnet/api/System.ISpanFormattable?view=net-7.0), [IFormattable](https://learn.microsoft.com/en-us/dotnet/api/System.IFormattable?view=net-7.0), [IConvertible](https://learn.microsoft.com/en-us/dotnet/api/System.IConvertible?view=net-7.0)_

### ⭐ Properties

#### IgnoreSoundFadeOnEnter

```csharp
public static const WorldFlags IgnoreSoundFadeOnEnter;
```

Reserved to indicate this world should skip the usual sound fade when entering it. Not currently read by any engine system.

**Returns** \
[WorldFlags](../../Murder/Assets/WorldFlags.html) \

#### IgnoreSoundFadeOnExit

```csharp
public static const WorldFlags IgnoreSoundFadeOnExit;
```

Reserved to indicate this world should skip the usual sound fade when exiting it. Not currently read by any engine system.

**Returns** \
[WorldFlags](../../Murder/Assets/WorldFlags.html) \

#### NeverPersist

```csharp
public static const WorldFlags NeverPersist;
```

This world's state is never written to a save slot. Checked by the save system to skip persisting worlds flagged this way.

**Returns** \
[WorldFlags](../../Murder/Assets/WorldFlags.html) \

#### None

```csharp
public static const WorldFlags None;
```

No special behavior; default transitions apply.

**Returns** \
[WorldFlags](../../Murder/Assets/WorldFlags.html) \

⚡
