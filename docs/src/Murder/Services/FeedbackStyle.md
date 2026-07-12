# FeedbackStyle

**Namespace:** Murder.Services \
**Assembly:** Murder.dll

```csharp
public enum FeedbackStyle : Enum, IComparable, ISpanFormattable, IFormattable, IConvertible
```

Identifies the kind of feedback endpoint suffix to target. Declared as a nested type of [FeedbackServices](../../Murder/Services/FeedbackServices.html).

**Intent:** Provides the value used (via `.ToString().ToLower()`) to build the endpoint URL suffix in `SendSaveDataFeedbackAsync` (`$"{Game.FeedbackUrl}{FeedbackStyle.Save.ToString().ToLower()}"`), so the same base feedback URL can route different report categories to different server-side handlers.

**Use-case:** Currently only `Save` is used internally by `FeedbackServices.SendSaveDataFeedbackAsync`; `Crash` is reserved for routing crash reports through the same URL-suffix convention, for a crash-handling flow that composes its own `RawFeedbackData` and posts through `SendFeedbackAsync`.

**Implements:** _[Enum](https://learn.microsoft.com/en-us/dotnet/api/System.Enum?view=net-7.0), [IComparable](https://learn.microsoft.com/en-us/dotnet/api/System.IComparable?view=net-7.0), [ISpanFormattable](https://learn.microsoft.com/en-us/dotnet/api/System.ISpanFormattable?view=net-7.0), [IFormattable](https://learn.microsoft.com/en-us/dotnet/api/System.IFormattable?view=net-7.0), [IConvertible](https://learn.microsoft.com/en-us/dotnet/api/System.IConvertible?view=net-7.0)_

### ⭐ Properties

#### Crash

```csharp
public static const FeedbackStyle Crash;
```

Identifies a crash-report style feedback submission.

**Returns** \
[FeedbackStyle](../../Murder/Services/FeedbackStyle.html) \

#### Save

```csharp
public static const FeedbackStyle Save;
```

Identifies a save-data/player-feedback style submission; used by `FeedbackServices.SendSaveDataFeedbackAsync` to build its target URL.

**Returns** \
[FeedbackStyle](../../Murder/Services/FeedbackStyle.html) \

⚡
