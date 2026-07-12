# LocalizationFlags

**Namespace:** Murder.Services \
**Assembly:** Murder.dll

```csharp
[Flags]
public enum LocalizationFlags : Enum, IComparable, ISpanFormattable, IFormattable, IConvertible
```

Options that modify how a localized string is resolved by [LocalizationServices](../../Murder/Services/LocalizationServices.html).

**Intent:** Lets callers opt in to bypassing the player's currently selected language and force the default/fallback localization instead, without needing a second, parallel set of "always default" lookup methods.

**Use-case:** Pass `LocalizationFlags.ForceDefault` to localization lookup methods when a string must always render in the game's default language regardless of the active locale — for example, developer/debug text, or content that hasn't been translated and should predictably fall back rather than show a missing-key placeholder.

**Implements:** _[Enum](https://learn.microsoft.com/en-us/dotnet/api/System.Enum?view=net-7.0), [IComparable](https://learn.microsoft.com/en-us/dotnet/api/System.IComparable?view=net-7.0), [ISpanFormattable](https://learn.microsoft.com/en-us/dotnet/api/System.ISpanFormattable?view=net-7.0), [IFormattable](https://learn.microsoft.com/en-us/dotnet/api/System.IFormattable?view=net-7.0), [IConvertible](https://learn.microsoft.com/en-us/dotnet/api/System.IConvertible?view=net-7.0)_

### ⭐ Properties

#### None

```csharp
public static const LocalizationFlags None;
```

Default behavior: resolve the string using the player's currently active localization.

**Returns** \
[LocalizationFlags](../../Murder/Services/LocalizationFlags.html) \

#### ForceDefault

```csharp
public static const LocalizationFlags ForceDefault;
```

Forces resolution against the default/fallback localization asset instead of the player's active language selection.

**Returns** \
[LocalizationFlags](../../Murder/Services/LocalizationFlags.html) \

⚡
