# LocalizedStringData

**Namespace:** Murder.Assets.Localization \
**Assembly:** Murder.dll

```csharp
public sealed struct LocalizedStringData
```

Stores the translated text and metadata for a single localized string entry within a `LocalizationAsset`.

**Intent:** Hold the actual translated string, reference count, translator notes, and a flag indicating whether the entry was machine-generated rather than hand-translated.

**Use-case:** Inspect `LocalizedStringData.String` to read a translated string by GUID, check `IsGenerated` to distinguish auto-translated entries from human-verified ones, and read `Notes` for context provided to translators.

### ⭐ Constructors
```csharp
public LocalizedStringData()
```

```csharp
public LocalizedStringData(Guid guid)
```

**Parameters** \
`guid` [Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \

### ⭐ Properties
#### Counter
```csharp
public T? Counter { get; public set; }
```

Total of references to this string data.

**Returns** \
[T?](https://learn.microsoft.com/en-us/dotnet/api/System.Nullable-1?view=net-7.0) \
#### Guid
```csharp
public readonly Guid Guid;
```

Unique identifier that links this data entry to its corresponding `LocalizedString.Id`.

**Returns** \
[Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \
#### IsGenerated
```csharp
public bool IsGenerated { get; public set; }
```

True when this entry was generated automatically (e.g. machine-translated) rather than hand-authored.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
#### Notes
```csharp
public string Notes { get; public set; }
```

Any notes relevant to this string.

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
#### String
```csharp
public string String { get; public set; }
```

The translated text for this entry in the locale of the owning `LocalizationAsset`.

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \


⚡