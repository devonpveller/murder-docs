# MurderFontServices

**Namespace:** Murder.Services \
**Assembly:** Murder.dll

```csharp
public static class MurderFontServices
```

Provides utilities for measuring text width using the engine's built-in font system.

**Intent:** Allows game code to query the pixel width of a string before rendering it, enabling layout calculations.

**Use-case:** Use `GetLineWidth` before calling `RenderServices.DrawText` to centre a label, truncate overflowing text, or align UI elements based on their text content.

### ⭐ Methods
#### GetLineWidth(MurderFonts, ReadOnlySpan<T>)
```csharp
public float GetLineWidth(MurderFonts font, ReadOnlySpan<T> text)
```
Returns the pixel width of `text` when rendered with the given `MurderFonts` font (span overload for zero-allocation calls).

**Parameters** \
`font` [MurderFonts](../../Murder/Services/MurderFonts.html) \
`text` [ReadOnlySpan\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.ReadOnlySpan-1?view=net-7.0) \

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### GetLineWidth(MurderFonts, string)
```csharp
public float GetLineWidth(MurderFonts font, string text)
```
Returns the pixel width of `text` when rendered with the given `MurderFonts` font.

**Parameters** \
`font` [MurderFonts](../../Murder/Services/MurderFonts.html) \
`text` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### GetLineWidth(int, string)
```csharp
public float GetLineWidth(int font, string text)
```
Returns the pixel width of `text` when rendered with the font identified by its integer index.

**Parameters** \
`font` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`text` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \



⚡