# LocalizedString

**Namespace:** Murder.Assets \
**Assembly:** Murder.dll

```csharp
public sealed struct LocalizedString
```

A lightweight string key that is resolved to localized text at runtime via the active `LocalizationAsset`.

**Intent:** Decouple content strings from their translations by storing only a GUID reference (or an optional inline override), so the same dialogue and UI data works across all supported languages.

**Use-case:** Use a `LocalizedString` anywhere a displayed string is needed. Assign its `Id` in the editor to point at an entry in the localization asset, or set `OverrideText` to bypass translation for dynamically generated strings. Cast the struct to `string` to resolve it against the active locale at runtime.

### ⭐ Constructors
```csharp
public LocalizedString()
```

```csharp
public LocalizedString(Guid id)
```

**Parameters** \
`id` [Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \

```csharp
public LocalizedString(string overrideText)
```

**Parameters** \
`overrideText` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

### ⭐ Properties
#### Id
```csharp
public readonly Guid Id;
```

The GUID key used to look up the translated string in the active `LocalizationAsset`.

**Returns** \
[Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \
#### OverrideText
```csharp
public readonly string OverrideText;
```

Used when, for whatever reason, we need to override the data for a localized string
            with actual text (usually built in runtime).

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \


⚡