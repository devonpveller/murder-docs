# LocalizedDialogueData

**Namespace:** Murder.Assets.Localization \
**Assembly:** Murder.dll

```csharp
public sealed struct LocalizedDialogueData
```

A single dialogue line's localized-string GUID paired with the GUID of the speaker who says it.

**Intent:** Produced by the dialogue import pipeline (e.g. the Gum-to-Murder converter) and stored inside [ResourceDataForAsset](../../../Murder/Assets/Localization/ResourceDataForAsset.html)'s `DataResources`, so the localization system and export tools know both what a translated line's text is and who speaks it, without needing to re-parse the dialogue script itself.

**Use-case:** Iterate `LocalizationAsset.FetchResourcesForDialogue(Guid)` to enumerate every line (and speaker) belonging to a dialogue asset, and cross-reference each entry's `Guid` against `LocalizationAsset.TryGetResource` to fetch the actual translated text. `LocalizationAsset.SetResourcesForDialogue` uses this struct's GUID-only equality to diff an old and new set of dialogue lines when a script is re-imported.

### ⭐ Constructors

```csharp
public LocalizedDialogueData(Guid speaker, Guid guid)
```

Creates a pairing between a dialogue line's localized-string GUID and the GUID of its speaker.

**Parameters** \
`speaker` [Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \
`guid` [Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \

### ⭐ Properties

#### Guid

```csharp
public readonly Guid Guid;
```

Guid for the string itself — the identifier of the `LocalizedStringData` entry holding this dialogue line's text.

**Returns** \
[Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \

#### Speaker

```csharp
public readonly Guid Speaker;
```

Guid for the speaker — identifies which character says this line.

**Returns** \
[Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \

### ⭐ Methods

#### GetHashCode()

```csharp
public override int GetHashCode()
```

Hashes by `Guid` only, so a `HashSet<LocalizedDialogueData>` of entries treats two lines with the same string GUID as duplicates regardless of speaker.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### Equals(object)

```csharp
public override bool Equals(object d)
```

Equality is based solely on `Guid` (the string identity), matching `GetHashCode()`. This is what lets `LocalizationAsset.SetResourcesForDialogue` diff an old and new set of dialogue lines by GUID alone.

**Parameters** \
`d` [object](https://learn.microsoft.com/en-us/dotnet/api/System.Object?view=net-7.0) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

⚡
