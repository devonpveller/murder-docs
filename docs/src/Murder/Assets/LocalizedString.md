# LocalizedString

**Namespace:** Murder.Assets \
**Assembly:** Murder.dll

```csharp
public sealed struct LocalizedString
```

A lightweight, serializable reference to a piece of translated text.

**Intent:** Instead of storing the string itself, gameplay/dialogue data stores a `LocalizedString` pointing at a GUID entry in the active `LocalizationAsset` (via `Id`), so the same data works unmodified across every language the game supports.

**Use-case:** Use a `LocalizedString` anywhere a displayed string is needed and must be translatable, e.g. `WorldAsset.LocalizedWorldName` or dialogue `Line` text. Assign its `Id` in the editor to point at an entry in the localization asset, or construct one from a plain `string` (setting `OverrideText`) to bypass translation for dynamically generated text. Cast the struct to `string`, call `ToString()`, or use `LocalizationServices` to resolve it against the active locale at runtime.

### ⭐ Constructors

```csharp
public LocalizedString()
```

Creates an empty localized string (no `Id`, no `OverrideText`) that resolves to an empty string.

```csharp
public LocalizedString(Guid id)
```

Creates a localized string that resolves through the localization asset using `id`. This is what the editor stores when a writer selects an entry in the localization asset.

**Parameters** \
`id` [Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \

```csharp
public LocalizedString(string overrideText)
```

Creates a localized string that bypasses translation entirely and always resolves to `overrideText` verbatim. Intended for text built dynamically at runtime (e.g. interpolated debug/UI strings) rather than for content that should be translated.

**Parameters** \
`overrideText` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

### ⭐ Properties

#### Id

```csharp
public readonly Guid Id;
```

GUID key used to look up the translated text for this string in the active `LocalizationAsset`. `Guid.Empty` means this instance has no localization entry and resolves to an empty string unless `OverrideText` is set.

**Returns** \
[Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \

#### OverrideText

```csharp
public readonly string OverrideText;
```

Used when, for whatever reason, we need to override the data for a localized string with actual text (usually built in runtime).

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

### ⭐ Methods

#### ToString()

```csharp
public override string ToString()
```

Resolves this instance to plain text for the currently active locale via `LocalizationServices.GetLocalizedString`.

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### ToInvariantString()

```csharp
public string ToInvariantString()
```

Resolves this instance to plain text using the game's default/invariant locale, ignoring whatever locale is currently active. Useful for logging, editor tooling, or any context that must not depend on the player's language setting.

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

⚡
