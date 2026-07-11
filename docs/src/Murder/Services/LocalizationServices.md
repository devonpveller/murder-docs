# LocalizationServices

**Namespace:** Murder.Services \
**Assembly:** Murder.dll

```csharp
public static class LocalizationServices
```

Provides methods for retrieving the current localization asset and translating `LocalizedString` values.

**Intent:** Abstracts locale-aware string resolution so game code always receives the correct translated text.

**Use-case:** Call `GetLocalizedString` anywhere you need to display player-facing text, and `GetCurrentLocalization` when you need access to the full localization data for the active language.

### ⭐ Methods
#### GetCurrentLocalization()
```csharp
public LocalizationAsset GetCurrentLocalization()
```
Returns the `LocalizationAsset` for the currently selected language.

**Returns** \
[LocalizationAsset](../../Murder/Assets/Localization/LocalizationAsset.html) \

#### GetLocalizedString(LocalizedString)
```csharp
public string GetLocalizedString(LocalizedString localized)
```
Returns the translated text for the given `LocalizedString` in the active language.

**Parameters** \
`localized` [LocalizedString](../../Murder/Assets/LocalizedString.html) \

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### TryGetLocalizedString(T?)
```csharp
public string TryGetLocalizedString(T? localized)
```
Safely returns the translated text for a nullable `LocalizedString`, or an empty string if it is `null`.

**Parameters** \
`localized` [T?](https://learn.microsoft.com/en-us/dotnet/api/System.Nullable-1?view=net-7.0) \

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \



⚡