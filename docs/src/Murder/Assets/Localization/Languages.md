# Languages

**Namespace:** Murder.Assets.Localization \
**Assembly:** Murder.dll

```csharp
public static class Languages
```

Static registry of all languages supported out-of-the-box by the engine, providing lookup helpers for `LanguageId`-keyed operations.

**Intent:** Centralize the mapping between [LanguageId](../../../Murder/Assets/Localization/LanguageId.html) enum values and their BCP-47 locale strings in one place, so the editor and `GameDataManager` can enumerate/cycle through supported languages consistently instead of scattering locale string literals across the codebase.

**Use-case:** Call `Languages.TryGet(LanguageId)` to resolve a `LanguageId` to its full [LanguageIdData](../../../Murder/Assets/Localization/LanguageIdData.html) (including the locale string), or iterate `Languages.All` to populate a language-selection UI in the editor. `GameDataManager.ChangeLanguage(LanguageId)` uses `TryGet` to validate a requested language before switching to it, failing gracefully (logging and ignoring) if the id is unsupported.

### ⭐ Properties

#### All

```csharp
public static LanguageIdData[] All { get; }
```

All registered languages, in the declaration order used to index `LanguageId` values. Lazily built and cached on first access.

**Returns** \
[LanguageIdData[]](../../../Murder/Assets/Localization/LanguageIdData.html) \

#### English

```csharp
public readonly static LanguageIdData English;
```

English (en-US) locale data. This is the language `GameDataManager.CurrentLocalization` defaults to and the one `GameDataManager.GetDefaultLocalization()` always falls back to when a translation is missing.

**Returns** \
[LanguageIdData](../../../Murder/Assets/Localization/LanguageIdData.html) \

#### Portuguese

```csharp
public readonly static LanguageIdData Portuguese;
```

Portuguese (pt-BR) locale data.

**Returns** \
[LanguageIdData](../../../Murder/Assets/Localization/LanguageIdData.html) \

#### Japanese

```csharp
public readonly static LanguageIdData Japanese;
```

Japanese (ja) locale data.

**Returns** \
[LanguageIdData](../../../Murder/Assets/Localization/LanguageIdData.html) \

#### Chinese

```csharp
public readonly static LanguageIdData Chinese;
```

Simplified Chinese (zh-Hans) locale data.

**Returns** \
[LanguageIdData](../../../Murder/Assets/Localization/LanguageIdData.html) \

#### TraditionalChinese

```csharp
public readonly static LanguageIdData TraditionalChinese;
```

Traditional Chinese (zh-Hant) locale data.

**Returns** \
[LanguageIdData](../../../Murder/Assets/Localization/LanguageIdData.html) \

#### French

```csharp
public readonly static LanguageIdData French;
```

French (fr) locale data.

**Returns** \
[LanguageIdData](../../../Murder/Assets/Localization/LanguageIdData.html) \

#### Italian

```csharp
public readonly static LanguageIdData Italian;
```

Italian (it) locale data.

**Returns** \
[LanguageIdData](../../../Murder/Assets/Localization/LanguageIdData.html) \

#### German

```csharp
public readonly static LanguageIdData German;
```

German (de) locale data.

**Returns** \
[LanguageIdData](../../../Murder/Assets/Localization/LanguageIdData.html) \

#### SpanishSpain

```csharp
public readonly static LanguageIdData SpanishSpain;
```

Spanish, Spain (es-ES) locale data.

**Returns** \
[LanguageIdData](../../../Murder/Assets/Localization/LanguageIdData.html) \

#### SpanishLatam

```csharp
public readonly static LanguageIdData SpanishLatam;
```

Spanish, Latin America (es-LATAM) locale data.

**Returns** \
[LanguageIdData](../../../Murder/Assets/Localization/LanguageIdData.html) \

#### Korean

```csharp
public readonly static LanguageIdData Korean;
```

Korean (ko) locale data.

**Returns** \
[LanguageIdData](../../../Murder/Assets/Localization/LanguageIdData.html) \

#### Russian

```csharp
public readonly static LanguageIdData Russian;
```

Russian (ru) locale data.

**Returns** \
[LanguageIdData](../../../Murder/Assets/Localization/LanguageIdData.html) \

#### Turkish

```csharp
public readonly static LanguageIdData Turkish;
```

Turkish (tr) locale data.

**Returns** \
[LanguageIdData](../../../Murder/Assets/Localization/LanguageIdData.html) \

#### Ukrainian

```csharp
public readonly static LanguageIdData Ukrainian;
```

Ukrainian (uk) locale data.

**Returns** \
[LanguageIdData](../../../Murder/Assets/Localization/LanguageIdData.html) \

#### Hungarian

```csharp
public readonly static LanguageIdData Hungarian;
```

Hungarian (hu) locale data.

**Returns** \
[LanguageIdData](../../../Murder/Assets/Localization/LanguageIdData.html) \

### ⭐ Methods

#### TryGet(LanguageId)

```csharp
public static LanguageIdData? TryGet(LanguageId id)
```

Attempts to resolve a `LanguageId` to its full `LanguageIdData` (including the BCP-47 locale string). Returns null instead of throwing when `id` falls outside the registered range, which lets callers such as `GameDataManager.ChangeLanguage(LanguageId)` fail gracefully (e.g. log and ignore) rather than crash when a save file references an unsupported id.

**Parameters** \
`id` [LanguageId](../../../Murder/Assets/Localization/LanguageId.html) \

**Returns** \
[LanguageIdData?](../../../Murder/Assets/Localization/LanguageIdData.html) \

⚡
