# LanguageId

**Namespace:** Murder.Assets.Localization \
**Assembly:** Murder.dll

```csharp
public sealed enum LanguageId : Enum, IComparable, ISpanFormattable, IFormattable, IConvertible
```

**Implements:** _[Enum](https://learn.microsoft.com/en-us/dotnet/api/System.Enum?view=net-7.0), [IComparable](https://learn.microsoft.com/en-us/dotnet/api/System.IComparable?view=net-7.0), [ISpanFormattable](https://learn.microsoft.com/en-us/dotnet/api/System.ISpanFormattable?view=net-7.0), [IFormattable](https://learn.microsoft.com/en-us/dotnet/api/System.IFormattable?view=net-7.0), [IConvertible](https://learn.microsoft.com/en-us/dotnet/api/System.IConvertible?view=net-7.0)_

Enumeration of supported game languages, used as keys in `GameProfile.LocalizationResources`.

**Intent:** Provide a type-safe integer index for each supported locale so that code can select and switch languages without hard-coding strings.

**Use-case:** Pass a `LanguageId` value to `Languages.Get` to retrieve the associated `LanguageIdData` (locale string), or store it in `GameProfile.LocalizationResources` as the key pointing to the correct `LocalizationAsset` GUID.

### ⭐ Properties
#### English
```csharp
public static const LanguageId English;
```

Identifier for the English (en-US) locale.

**Returns** \
[LanguageId](../../../Murder/Assets/Localization/LanguageId.html) \
#### Portuguese
```csharp
public static const LanguageId Portuguese;
```

Identifier for the Portuguese (pt-BR) locale.

**Returns** \
[LanguageId](../../../Murder/Assets/Localization/LanguageId.html) \


⚡