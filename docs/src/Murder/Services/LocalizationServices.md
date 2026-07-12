# LocalizationServices

**Namespace:** Murder.Services \
**Assembly:** Murder.dll

```csharp
public static class LocalizationServices
```

Provides methods for retrieving the current localization asset and translating `LocalizedString` values into player-facing text.

**Intent:** Abstracts locale-aware string resolution so game code and UI systems always fetch translated text for the active language without having to know how localization assets and fallback resources are organized.

**Use-case:** Call `GetLocalizedString` (or the null-safe `TryGetLocalizedString`) anywhere you need to display text that was authored through the localization pipeline, and `GetCurrentLocalization` when you need direct access to the full `LocalizationAsset` for the active language (for example to enumerate every localized resource for a report or export tool).

### ⭐ Methods

#### GetCurrentLocalization()

```csharp
public static LocalizationAsset GetCurrentLocalization()
```

Returns the `LocalizationAsset` for the currently selected language, as tracked by `Game.Data.Localization`. Use this when you need the whole localization table rather than a single string.

**Returns** \
[LocalizationAsset](../../Murder/Assets/Localization/LocalizationAsset.html) \

#### GetLocalizedString(LocalizedString, LocalizationFlags)

```csharp
public static string GetLocalizedString(LocalizedString localized, LocalizationFlags flags = LocalizationFlags.None)
```

Resolves `localized` to the translated string for the active language. If `localized.OverrideText` is set, that literal text is returned as-is (used for ad-hoc, non-localized strings). Otherwise the resource is looked up by `localized.Id` in the current localization asset, falling back to the default localization if the current one is missing that resource; if neither has it, an empty string is returned and a warning is logged. Pass `LocalizationFlags.ForceDefault` to skip the active language entirely and resolve directly against the default localization (useful for tooling or diagnostics that always want the source-language text regardless of the player's language setting).

**Parameters** \
`localized` [LocalizedString](../../Murder/Assets/LocalizedString.html) \
`flags` `LocalizationFlags` \

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### IsTextWrapOnlyOnSpace()

```csharp
public static bool IsTextWrapOnlyOnSpace()
```

Returns `false` for languages that do not use spaces to separate words (currently Japanese and Chinese), and `true` otherwise. Used by the text-wrapping code in `PixelFont` to decide whether it is safe to break long lines only at whitespace, or whether it must be able to break between arbitrary characters instead.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### TryGetLocalizedString(LocalizedString?)

```csharp
public static string? TryGetLocalizedString(LocalizedString? localized)
```

Null-safe wrapper around `GetLocalizedString`: returns `null` when `localized` is `null`, and the resolved translated text otherwise. Convenient when the caller is dealing with an optional/nullable localized field (e.g. an entity component with an unset text) and wants to avoid an explicit null check before translating.

**Parameters** \
`localized` [LocalizedString?](../../Murder/Assets/LocalizedString.html) \

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

⚡
