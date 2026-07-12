# CreateWorldFlags

**Namespace:** Murder.Assets \
**Assembly:** Murder.dll

```csharp
public sealed enum CreateWorldFlags : Enum, IComparable, ISpanFormattable, IFormattable, IConvertible
```

Flags describing the circumstances under which a `World` is being created/entered.

**Intent:** Let `WorldAsset` and `WorldEventsAsset` preprocessing distinguish a fresh load from re-entering an already-initialized world, so one-time setup (like spawning global event watchers) only runs once.

**Use-case:** Passed internally by `WorldAsset.CreateInstance` when building a `MonoWorld`, and consumed by `WorldEventsAsset.Preprocess` (via `WorldEventsTracker.PreprocessWorldEvents`) to decide whether to (re)spawn its `Watchers`.

**Implements:** _[Enum](https://learn.microsoft.com/en-us/dotnet/api/System.Enum?view=net-7.0), [IComparable](https://learn.microsoft.com/en-us/dotnet/api/System.IComparable?view=net-7.0), [ISpanFormattable](https://learn.microsoft.com/en-us/dotnet/api/System.ISpanFormattable?view=net-7.0), [IFormattable](https://learn.microsoft.com/en-us/dotnet/api/System.IFormattable?view=net-7.0), [IConvertible](https://learn.microsoft.com/en-us/dotnet/api/System.IConvertible?view=net-7.0)_

### ⭐ Properties

#### AfterStarted

```csharp
public static const CreateWorldFlags AfterStarted;
```

The world is being (re)created after the game has already started running.

**Returns** \
[CreateWorldFlags](../../Murder/Assets/CreateWorldFlags.html) \

#### FirstTimeLoaded

```csharp
public static const CreateWorldFlags FirstTimeLoaded;
```

This is the first time this particular world instance is being loaded (not restored from a save/transition). `WorldEventsAsset.Preprocess` only spawns its watchers when this flag is set.

**Returns** \
[CreateWorldFlags](../../Murder/Assets/CreateWorldFlags.html) \

#### None

```csharp
public static const CreateWorldFlags None;
```

No special circumstances.

**Returns** \
[CreateWorldFlags](../../Murder/Assets/CreateWorldFlags.html) \

⚡
