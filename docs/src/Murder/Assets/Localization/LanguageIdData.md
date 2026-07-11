# LanguageIdData

**Namespace:** Murder.Assets.Localization \
**Assembly:** Murder.dll

```csharp
public sealed struct LanguageIdData
```

Pairs a `LanguageId` enum value with its BCP-47 locale identifier string (e.g. `"en-US"`).

**Intent:** Bundle the strongly-typed `LanguageId` with its corresponding locale string so that both can be retrieved from a single lookup.

**Use-case:** Obtain a `LanguageIdData` from `Languages.Get(LanguageId)` to read the `Identifier` string when configuring locale-sensitive systems or when reporting the active language to platform services.

### ⭐ Constructors
```csharp
public LanguageIdData(LanguageId id, string identifier)
```

**Parameters** \
`id` [LanguageId](../../../Murder/Assets/Localization/LanguageId.html) \
`identifier` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

### ⭐ Properties
#### Id
```csharp
public readonly LanguageId Id;
```

The `LanguageId` enum value identifying the language.

**Returns** \
[LanguageId](../../../Murder/Assets/Localization/LanguageId.html) \
#### Identifier
```csharp
public readonly string Identifier;
```

BCP-47 locale string (e.g. `"en-US"`, `"pt-BR"`) for this language.

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \


⚡