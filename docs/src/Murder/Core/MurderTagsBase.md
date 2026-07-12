# MurderTagsBase

**Namespace:** Murder.Core \
**Assembly:** Murder.dll

```csharp
public class MurderTagsBase
```

Base registry of the built-in bitfield tag constants Murder itself relies on to categorize entities.

**Intent:** A plain container of `const int` bit values (not a class meant to be instantiated or subclassed in the traditional sense) that reserves the first few tag bits for engine-recognized categories (e.g. the player, trigger volumes). Game projects that want additional tags declare their own set of `1 << n` constants starting after the bits already reserved here, following the same pattern, and combine them with `GridNumberExtensions.ToMask`/`HasFlag` the same way the engine does internally.

**Use-case:** Reference these constants when assigning a tags bitmask to an entity or when querying entities by tag in systems (e.g. checking `HasFlag(MurderTagsBase.PLAYER)` on an entity's tag component).

### ⭐ Constructors

```csharp
public MurderTagsBase()
```

This class should never be instanced; it only exists to hold the `const` tag values.

### ⭐ Properties

#### NONE

```csharp
public static const int NONE;
```

The empty tag value (0); no tags set.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### PLAYER

```csharp
public static const int PLAYER;
```

Tag bit identifying an entity as a player-controlled character.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### TRIGGER

```csharp
public static const int TRIGGER;
```

Tag bit identifying an entity as a trigger volume that fires interactions on contact.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

⚡
