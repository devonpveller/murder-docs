# LocalizedStringData

**Namespace:** Murder.Assets.Localization \
**Assembly:** Murder.dll

```csharp
public sealed struct LocalizedStringData
```

A single translated string entry stored inside a `LocalizationAsset`.

**Intent:** Each entry is keyed by `Guid`, which is the same id carried by a `LocalizedString` handle referenced from components/assets, so this is the record that actually resolves that handle into on-screen text for one specific locale.

**Use-case:** Inspect `LocalizedStringData.String` to read a translated string by GUID, check `IsGenerated` to distinguish auto-translated entries from human-verified ones, and read `Notes` for context provided to translators. `LocalizationAsset.TryGetResource` is the usual way to obtain one, and `LocalizationServices.GetLocalizedString` reads its `String` to resolve a `LocalizedString` at runtime.

### ⭐ Constructors

```csharp
public LocalizedStringData()
```

Creates an empty entry with a zero `Guid`. Exists so the struct has a public parameterless constructor for serialization and `with`-expression defaults.

```csharp
public LocalizedStringData(Guid guid)
```

Creates a new entry for the given `guid` with empty text, ready to be populated via a `with` expression (see `LocalizationAsset.AddResource(string, bool)`).

**Parameters** \
`guid` [Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \

### ⭐ Properties

#### Counter

```csharp
public T? Counter { get; public set; }
```

Reference count tracking how many places (components, dialogue lines, etc.) currently point at this string. `LocalizationAsset.AddResource(Guid)` increments it and `LocalizationAsset.RemoveResource(Guid, bool)` decrements it; when it reaches zero (or is null) the entry is eligible for removal, which lets the editor safely prune strings that are no longer referenced by anything in the game.

**Returns** \
[T?](https://learn.microsoft.com/en-us/dotnet/api/System.Nullable-1?view=net-7.0) \

#### Guid

```csharp
public readonly Guid Guid;
```

Unique identifier that links this data entry to its corresponding `LocalizedString.Id`. The same GUID is repeated across every `LocalizationAsset` (one per language) so the localization service can look up the equivalent translation regardless of the active language.

**Returns** \
[Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \

#### IsGenerated

```csharp
public bool IsGenerated { get; public set; }
```

True when this entry's `String` was produced automatically (e.g. copied from the default locale or machine-translated) rather than hand-authored/reviewed by a human translator. The editor uses this flag to visually flag entries that still need human review.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### Notes

```csharp
public string Notes { get; public set; }
```

Free-form notes attached to this string, typically written by a designer to give translators context (tone, character speaking, line length constraints, etc.) that the raw text alone doesn't convey.

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### String

```csharp
public string String { get; public set; }
```

The actual text for this entry, in the language of the owning `LocalizationAsset`. This is what gets shown to the player when a `LocalizedString` with this `Guid` is resolved.

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

⚡
