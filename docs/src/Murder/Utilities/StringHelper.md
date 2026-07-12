# StringHelper

**Namespace:** Murder.Utilities \
**Assembly:** Murder.dll

```csharp
public static partial class StringHelper
```

String utility methods for fuzzy/edit-distance matching, enum-to-display-name resolution, capitalization, whitespace normalization, and culture-invariant, exception-safe string formatting.

**Intent:** Used by editor search boxes, dialogue/localization display, and anywhere gameplay text is formatted from user- or designer-provided templates that shouldn't crash the game on a malformed format string.

**Use-case:** Use `FuzzyMatch` for search-box filtering, `LevenshteinDistance` for spell-checking/"did you mean" suggestions, `CapitalizeFirstLetter` for display formatting, `Cleanup` to normalize line breaks in imported text, `GetDescription`/`GetAttribute` to resolve friendly names for enum values, and `FormatSafe` instead of `string.Format` when the format string comes from designer/localization content.

### ⭐ Methods

#### FuzzyMatch(string, string)

```csharp
public bool FuzzyMatch(string searchTerm, string target)
```

Returns `true` if every space-separated word in `searchTerm` can be found, in order and case-insensitively, as a (possibly non-contiguous) subsequence of `target` starting after the previous word's match. An empty or whitespace-only `searchTerm` always matches. Used to power "fuzzy" search-as-you-type filtering (e.g. the editor's asset/component picker), where users expect partial, out-of-order-friendly substring matches rather than exact ones.

**Parameters** \
`searchTerm` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) — The (possibly multi-word) query typed by the user. \
`target` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) — The candidate string being tested against the query. \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) — `true` if all words of `searchTerm` fuzzy-match, in order, within `target`. \

#### LevenshteinDistance(string, string)

```csharp
public int LevenshteinDistance(string s, string t)
```

Computes the Levenshtein edit distance between `s` and `t` — the minimum number of single-character insertions, deletions, or substitutions needed to turn one string into the other. Lower values mean the strings are more similar; a distance of 0 means they're equal.

**Parameters** \
`s` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
`t` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) — The minimum edit distance between the two strings. \

#### GetAttribute(T)

```csharp
public TAttr? GetAttribute(T enumerationValue)
```

Returns the custom attribute of type `TAttr` declared on the specific enum member `enumerationValue` is set to (e.g. a `[Description]` or a custom engine attribute), or `default` if the member has no such attribute. More general than `GetDescription`, which is hard-coded to `DescriptionAttribute`.

**Parameters** \
`enumerationValue` [T](../../) \

**Returns** \
[TAttr](../../) \

#### GetDescription(T)

```csharp
public string GetDescription(T enumerationValue)
```

Returns the human-readable text from the enum member's `DescriptionAttribute`, or the member's own `ToString()` if it has none. Used to display friendly names for enum values in the editor UI without having to hand-maintain a separate name-lookup table.

**Parameters** \
`enumerationValue` [T](../../) \

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### Cleanup(string)

```csharp
public string Cleanup(string input)
```

Collapses single line breaks (a lone `\n` not adjacent to another) into a space, while leaving blank-line paragraph breaks (`\n\n`) untouched. Used to normalize text pasted or imported from sources that hard-wrap lines (e.g. spreadsheets, external dialogue tools) so it re-flows naturally instead of keeping the original line breaks.

**Parameters** \
`input` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) — The text to normalize. \

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) — The text with single line breaks replaced by spaces; paragraph breaks are preserved. \

#### ToHumanList(IEnumerable\<string\>, string, string)

```csharp
public string ToHumanList(IEnumerable<string> someStringArray, string separator, string lastItemSeparator)
```

Joins a list of strings into a natural-language list, e.g. `["a", "b", "c"]` with `separator` `","` and `lastItemSeparator` `"and"` becomes `"a, b and c"`. All items except the last are joined with `separator`; the final item is joined with `lastItemSeparator` instead. Used for grammatically correct display of dynamic lists (e.g. "You picked up a Sword, a Shield and a Potion").

**Parameters** \
`someStringArray` [IEnumerable\<string\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Generic.IEnumerable-1?view=net-7.0) — The items to join. \
`separator` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) — Separator used between all items except the last two. \
`lastItemSeparator` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) — Separator used between the second-to-last and last item (e.g. "and"). \

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### CapitalizeFirstLetter(string, StringHelperCapitalizeFlags)

```csharp
public string CapitalizeFirstLetter(string input, StringHelperCapitalizeFlags flags = StringHelperCapitalizeFlags.FirstOnly)
```

Capitalizes `input` according to `flags`: by default only the very first letter is upper-cased; with `StringHelperCapitalizeFlags.AfterSpace` every word is capitalized instead (optionally normalizing whitespace first via `StringHelperCapitalizeFlags.TrimSpaces`). Already-capitalized letters are left as-is. Used for display-name formatting (e.g. turning a raw asset/enum identifier into title text).

**Parameters** \
`input` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) — The text to capitalize. \
`flags` [StringHelperCapitalizeFlags](../../Murder/Utilities/StringHelper.html) — Which capitalization strategy to apply; defaults to `FirstOnly`. \

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) — The capitalized string, or `string.Empty` if `input` is null or empty. \

#### FormatSafe(string, object)

```csharp
public string FormatSafe(string toFormat, object? str1)
```

Behaves like `string.Format` (using `CultureInfo.InvariantCulture`), but never throws: if `toFormat` has a malformed composite format string (e.g. mismatched braces, an out-of-range placeholder), the error is logged and the original, unformatted `toFormat` string is returned instead of crashing. Used when formatting designer- or localization-authored template strings (dialogue, tooltips) where a typo in content shouldn't take down the game.

**Parameters** \
`toFormat` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
`str1` [object](https://learn.microsoft.com/en-us/dotnet/api/System.Object?view=net-7.0) \

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### FormatSafe(string, object, object)

```csharp
public string FormatSafe(string toFormat, object? str1, object? str2)
```

Two-argument overload of `FormatSafe(string, object)`; see that overload for behavior.

**Parameters** \
`toFormat` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
`str1` [object](https://learn.microsoft.com/en-us/dotnet/api/System.Object?view=net-7.0) \
`str2` [object](https://learn.microsoft.com/en-us/dotnet/api/System.Object?view=net-7.0) \

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### FormatSafe(string, object, object, object)

```csharp
public string FormatSafe(string toFormat, object? str1, object? str2, object? str3)
```

Three-argument overload of `FormatSafe(string, object)`; see that overload for behavior.

**Parameters** \
`toFormat` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
`str1` [object](https://learn.microsoft.com/en-us/dotnet/api/System.Object?view=net-7.0) \
`str2` [object](https://learn.microsoft.com/en-us/dotnet/api/System.Object?view=net-7.0) \
`str3` [object](https://learn.microsoft.com/en-us/dotnet/api/System.Object?view=net-7.0) \

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### FormatSafe(string, object, object, object, object)

```csharp
public string FormatSafe(string toFormat, object? str1, object? str2, object? str3, object? str4)
```

Four-argument overload of `FormatSafe(string, object)`; see that overload for behavior.

**Parameters** \
`toFormat` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
`str1` [object](https://learn.microsoft.com/en-us/dotnet/api/System.Object?view=net-7.0) \
`str2` [object](https://learn.microsoft.com/en-us/dotnet/api/System.Object?view=net-7.0) \
`str3` [object](https://learn.microsoft.com/en-us/dotnet/api/System.Object?view=net-7.0) \
`str4` [object](https://learn.microsoft.com/en-us/dotnet/api/System.Object?view=net-7.0) \

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

⚡
