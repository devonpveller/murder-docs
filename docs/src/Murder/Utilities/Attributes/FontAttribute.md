# FontAttribute

**Namespace:** Murder.Utilities.Attributes \
**Assembly:** Murder.dll

```csharp
public class FontAttribute : Attribute
```

Dual-purpose attribute for the engine's font system: marks either an enum of font indices, or an `int` field referencing one.

**Intent:** Lets the engine discover the set of available fonts by scanning enums, and lets a component/asset field reference a font by picking from that set in the editor instead of a raw integer id.

**Use-case:** Apply to an enum type such as `MurderFonts` to mark its constants as font indices; `AssetsFilter.Fonts` scans every enum carrying this attribute to build the combined list of selectable fonts. Apply to an `int` field (e.g. `SpeakerAsset`'s font override, or `ButtonStyle`'s font field) so the editor's `IntField` renders a font-picker dropdown backed by that list instead of a plain numeric input.

**Implements:** _[Attribute](https://learn.microsoft.com/en-us/dotnet/api/System.Attribute?view=net-7.0)_

### ⭐ Constructors

```csharp
public FontAttribute()
```

### ⭐ Properties

#### TypeId

```csharp
public virtual Object TypeId { get; }
```

Unique object identity for this attribute type, inherited from `Attribute`.

**Returns** \
[Object](https://learn.microsoft.com/en-us/dotnet/api/System.Object?view=net-7.0) \

⚡
