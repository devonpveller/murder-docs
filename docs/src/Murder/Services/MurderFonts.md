# MurderFonts

**Namespace:** Murder.Services \
**Assembly:** Murder.dll

```csharp
public sealed enum MurderFonts : Enum, IComparable, ISpanFormattable, IFormattable, IConvertible
```

Enumerates the built-in font slots available in the Murder engine.

**Intent:** Provides named constants for referencing engine-managed pixel fonts, instead of passing raw integer font indices around. The enum is marked with the `[Font]` attribute so the editor can present these values as a font picker for fields typed as `int` that represent a font index.

**Use-case:** Pass `MurderFonts.PixelFont`, `MurderFonts.LargeFont`, or `MurderFonts.SmallFont` to `RenderServices.DrawText`/`DrawSimpleText` or the `MurderFontServices` measurement helpers instead of a magic integer. The underlying integer values (100, 101, 102) are looked up via `Game.Data.GetFont` to resolve the actual `PixelFont` asset.

**Implements:** _[Enum](https://learn.microsoft.com/en-us/dotnet/api/System.Enum?view=net-7.0), [IComparable](https://learn.microsoft.com/en-us/dotnet/api/System.IComparable?view=net-7.0), [ISpanFormattable](https://learn.microsoft.com/en-us/dotnet/api/System.ISpanFormattable?view=net-7.0), [IFormattable](https://learn.microsoft.com/en-us/dotnet/api/System.IFormattable?view=net-7.0), [IConvertible](https://learn.microsoft.com/en-us/dotnet/api/System.IConvertible?view=net-7.0)_

### ⭐ Properties

#### LargeFont

```csharp
public static const MurderFonts LargeFont = 101;
```

A larger pixel font intended for titles, headings, or emphasis text.

**Returns** \
[MurderFonts](../../Murder/Services/MurderFonts.html) \

#### PixelFont

```csharp
public static const MurderFonts PixelFont = 100;
```

The default small pixel font used for body text and dialogue.

**Returns** \
[MurderFonts](../../Murder/Services/MurderFonts.html) \

#### SmallFont

```csharp
public static const MurderFonts SmallFont = 102;
```

A smaller pixel font, useful where space is tight (e.g. compact HUD labels or footnote-style text).

**Returns** \
[MurderFonts](../../Murder/Services/MurderFonts.html) \

⚡
