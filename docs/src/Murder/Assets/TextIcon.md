# TextIcon

**Namespace:** Murder.Assets \
**Assembly:** Murder.dll

```csharp
public readonly struct TextIcon
```

Associates a lookup identifier with a `Portrait` image so it can be embedded inline within rendered text (dialogue lines, story text, etc.).

**Intent:** Provide a lightweight, serializable mapping between a text-placeholder ID and the small image that should be drawn in its place, so writers can reference icons (e.g. a coin, a key, a character's face) directly from dialogue strings without hard-coding sprite GUIDs.

**Use-case:** Add entries to `TextIconsAsset.Icons` in the editor, each with a short, memorable `Id`. When the text renderer encounters a matching icon placeholder while drawing a string, it calls `TextIconsAsset.TryFetchIcon(id)` to resolve this struct's `Portrait` and draws it in place of the placeholder. Icons are constrained to a small width (no more than roughly 6 pixels, sized relative to the 'M' character) so they read well inline with the font.

### ⭐ Constructors

```csharp
public TextIcon()
```

Creates an icon entry with an empty ID and an empty (unset) portrait, ready to be filled in via the editor.

### ⭐ Properties

#### Id

```csharp
public readonly string Id;
```

Identifier used to reference this icon from an in-text icon placeholder. Lookups against this ID are case-insensitive.

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### Portrait

```csharp
public readonly Portrait Portrait;
```

The portrait image drawn in place of the icon placeholder when this icon is resolved.

**Returns** \
[Portrait](../../Murder/Core/Portrait.html) \

⚡
