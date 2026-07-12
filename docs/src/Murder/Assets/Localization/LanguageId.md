# LanguageId

**Namespace:** Murder.Assets.Localization \
**Assembly:** Murder.dll

```csharp
public sealed enum LanguageId : Enum, IComparable, ISpanFormattable, IFormattable, IConvertible
```

**Implements:** _[Enum](https://learn.microsoft.com/en-us/dotnet/api/System.Enum?view=net-7.0), [IComparable](https://learn.microsoft.com/en-us/dotnet/api/System.IComparable?view=net-7.0), [ISpanFormattable](https://learn.microsoft.com/en-us/dotnet/api/System.ISpanFormattable?view=net-7.0), [IFormattable](https://learn.microsoft.com/en-us/dotnet/api/System.IFormattable?view=net-7.0), [IConvertible](https://learn.microsoft.com/en-us/dotnet/api/System.IConvertible?view=net-7.0)_

Enumeration of all languages supported out-of-the-box by the engine.

**Intent:** Provide a type-safe key for each supported locale so code, save data, and asset references can select a language without hard-coding locale strings. The underlying integer values also double as the index into [Languages.All](../../../Murder/Assets/Localization/Languages.html), so members must stay contiguous starting at `0`.

**Use-case:** Used as the key type for `GameProfile.LocalizationResources` (which maps each language to the GUID of its [LocalizationAsset](../../../Murder/Assets/Localization/LocalizationAsset.html)), and passed to `GameDataManager.ChangeLanguage` / `GamePreferences.SetLanguage` to change or persist the game's active language. Pass a `LanguageId` value to [Languages.TryGet](../../../Murder/Assets/Localization/Languages.html) to resolve its [LanguageIdData](../../../Murder/Assets/Localization/LanguageIdData.html) (BCP-47 locale string).

### ⭐ Properties

#### English

```csharp
public static const LanguageId English;
```

English (en-US). The default/fallback language used by `GameDataManager.GetDefaultLocalization()` whenever the active language's [LocalizationAsset](../../../Murder/Assets/Localization/LocalizationAsset.html) is missing an entry.

**Returns** \
[LanguageId](../../../Murder/Assets/Localization/LanguageId.html) \

#### Portuguese

```csharp
public static const LanguageId Portuguese;
```

Portuguese (pt-BR).

**Returns** \
[LanguageId](../../../Murder/Assets/Localization/LanguageId.html) \

#### Japanese

```csharp
public static const LanguageId Japanese;
```

Japanese (ja). Checked by `LocalizationServices.IsTextWrapOnlyOnSpace` to disable space-only text wrapping for this language.

**Returns** \
[LanguageId](../../../Murder/Assets/Localization/LanguageId.html) \

#### Chinese

```csharp
public static const LanguageId Chinese;
```

Simplified Chinese (zh-Hans). Checked by `LocalizationServices.IsTextWrapOnlyOnSpace` to disable space-only text wrapping for this language.

**Returns** \
[LanguageId](../../../Murder/Assets/Localization/LanguageId.html) \

#### TraditionalChinese

```csharp
public static const LanguageId TraditionalChinese;
```

Traditional Chinese (zh-Hant).

**Returns** \
[LanguageId](../../../Murder/Assets/Localization/LanguageId.html) \

#### French

```csharp
public static const LanguageId French;
```

French (fr).

**Returns** \
[LanguageId](../../../Murder/Assets/Localization/LanguageId.html) \

#### Italian

```csharp
public static const LanguageId Italian;
```

Italian (it).

**Returns** \
[LanguageId](../../../Murder/Assets/Localization/LanguageId.html) \

#### German

```csharp
public static const LanguageId German;
```

German (de).

**Returns** \
[LanguageId](../../../Murder/Assets/Localization/LanguageId.html) \

#### SpanishSpain

```csharp
public static const LanguageId SpanishSpain;
```

Spanish, Spain (es-ES).

**Returns** \
[LanguageId](../../../Murder/Assets/Localization/LanguageId.html) \

#### SpanishLatam

```csharp
public static const LanguageId SpanishLatam;
```

Spanish, Latin America (es-LATAM).

**Returns** \
[LanguageId](../../../Murder/Assets/Localization/LanguageId.html) \

#### Korean

```csharp
public static const LanguageId Korean;
```

Korean (ko).

**Returns** \
[LanguageId](../../../Murder/Assets/Localization/LanguageId.html) \

#### Russian

```csharp
public static const LanguageId Russian;
```

Russian (ru).

**Returns** \
[LanguageId](../../../Murder/Assets/Localization/LanguageId.html) \

#### Turkish

```csharp
public static const LanguageId Turkish;
```

Turkish (tr).

**Returns** \
[LanguageId](../../../Murder/Assets/Localization/LanguageId.html) \

#### Ukrainian

```csharp
public static const LanguageId Ukrainian;
```

Ukrainian (uk).

**Returns** \
[LanguageId](../../../Murder/Assets/Localization/LanguageId.html) \

#### Hungarian

```csharp
public static const LanguageId Hungarian;
```

Hungarian (hu).

**Returns** \
[LanguageId](../../../Murder/Assets/Localization/LanguageId.html) \

⚡
