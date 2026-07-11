# MurderFonts

**Namespace:** Murder.Services \
**Assembly:** Murder.dll

```csharp
public sealed enum MurderFonts : Enum, IComparable, ISpanFormattable, IFormattable, IConvertible
```

Enumerates the built-in font slots available in the Murder engine.

**Intent:** Provides named constants for referencing engine-managed pixel fonts by index.

**Use-case:** Pass `MurderFonts.PixelFont` or `MurderFonts.LargeFont` to `RenderServices.DrawText` or `MurderFontServices` helpers instead of using magic integer indices.

**Implements:** _[Enum](https://learn.microsoft.com/en-us/dotnet/api/System.Enum?view=net-7.0), [IComparable](https://learn.microsoft.com/en-us/dotnet/api/System.IComparable?view=net-7.0), [ISpanFormattable](https://learn.microsoft.com/en-us/dotnet/api/System.ISpanFormattable?view=net-7.0), [IFormattable](https://learn.microsoft.com/en-us/dotnet/api/System.IFormattable?view=net-7.0), [IConvertible](https://learn.microsoft.com/en-us/dotnet/api/System.IConvertible?view=net-7.0)_

### ⭐ Properties
#### LargeFont
```csharp
public static const MurderFonts LargeFont;
```
A larger pixel font for titles, headings, or emphasis text.

**Returns** \
[MurderFonts](../../Murder/Services/MurderFonts.html) \
#### PixelFont
```csharp
public static const MurderFonts PixelFont;
```
The default small pixel font used for body text and dialogue.

**Returns** \
[MurderFonts](../../Murder/Services/MurderFonts.html) \


⚡