# Languages

**Namespace:** Murder.Assets.Localization \
**Assembly:** Murder.dll

```csharp
public static class Languages
```

Static registry of all supported `LanguageIdData` entries, providing lookup helpers for `LanguageId`-keyed operations.

**Intent:** Centralise the mapping between `LanguageId` enum values and their BCP-47 locale strings in one place, avoiding scattered string literals across the codebase.

**Use-case:** Call `Languages.Get(LanguageId)` to retrieve locale metadata for the active language, or iterate `Languages.All` to populate a language-selection UI. Use `Languages.Next` to cycle through available languages.

### ⭐ Properties
#### All
```csharp
public static LanguageIdData[] All { get; }
```

Returns all registered language entries in declaration order.

**Returns** \
[LanguageIdData[]](../../../Murder/Assets/Localization/LanguageIdData.html) \
#### English
```csharp
public readonly static LanguageIdData English;
```

Predefined data entry for the English (en-US) locale.

**Returns** \
[LanguageIdData](../../../Murder/Assets/Localization/LanguageIdData.html) \
#### Portuguese
```csharp
public readonly static LanguageIdData Portuguese;
```

Predefined data entry for the Portuguese (pt-BR) locale.

**Returns** \
[LanguageIdData](../../../Murder/Assets/Localization/LanguageIdData.html) \
### ⭐ Methods
#### Get(LanguageId)
```csharp
public LanguageIdData Get(LanguageId id)
```

Retrieves the `LanguageIdData` for the given `LanguageId`.

**Parameters** \
`id` [LanguageId](../../../Murder/Assets/Localization/LanguageId.html) \

**Returns** \
[LanguageIdData](../../../Murder/Assets/Localization/LanguageIdData.html) \

#### Next(LanguageId)
```csharp
public LanguageIdData Next(LanguageId id)
```

Returns the `LanguageIdData` for the language that follows `id` in the declared order, wrapping around to the first entry.

**Parameters** \
`id` [LanguageId](../../../Murder/Assets/Localization/LanguageId.html) \

**Returns** \
[LanguageIdData](../../../Murder/Assets/Localization/LanguageIdData.html) \



⚡