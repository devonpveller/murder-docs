# LanguageIdData

**Namespace:** Murder.Assets.Localization \
**Assembly:** Murder.dll

```csharp
public sealed struct LanguageIdData
```

Pairs a [LanguageId](../../../Murder/Assets/Localization/LanguageId.html) enum value with its BCP-47 locale identifier string (e.g. `"en-US"`).

**Intent:** The enum alone is only useful for switch statements and dictionary keys; this struct carries the human/OS-facing locale string alongside it, so both can be obtained from a single lookup instead of maintaining a second string-literal table.

**Use-case:** Obtain a `LanguageIdData` from [Languages.TryGet(LanguageId)](../../../Murder/Assets/Localization/Languages.html) or one of its static fields (e.g. `Languages.English`) to read the `Identifier` string when exporting localization data or interfacing with platform/OS locale APIs. `GameDataManager.CurrentLocalization` exposes the active language as a `LanguageIdData`.

### ⭐ Constructors

```csharp
public LanguageIdData(LanguageId id, string identifier)
```

Creates a new pairing of a `LanguageId` with its locale identifier string. Used internally by [Languages](../../../Murder/Assets/Localization/Languages.html) to build its static registry entries; game code normally reads the existing static fields (`Languages.English`, etc.) rather than constructing new instances.

**Parameters** \
`id` [LanguageId](../../../Murder/Assets/Localization/LanguageId.html) \
`identifier` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

### ⭐ Properties

#### Id

```csharp
public readonly LanguageId Id;
```

The strongly-typed identifier for the language, used as a dictionary key (e.g. in `GameProfile.LocalizationResources`) and for equality checks.

**Returns** \
[LanguageId](../../../Murder/Assets/Localization/LanguageId.html) \

#### Identifier

```csharp
public readonly string Identifier;
```

BCP-47 locale string (e.g. `"en-US"`, `"pt-BR"`) identifying this language/region pair. Used when exporting localization data or interfacing with platform/OS locale APIs.

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

⚡
