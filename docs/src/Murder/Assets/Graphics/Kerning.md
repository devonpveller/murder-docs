# Kerning

**Namespace:** Murder.Assets.Graphics \
**Assembly:** Murder.dll

```csharp
public sealed struct Kerning
```

Represents a single kerning pair that adjusts the spacing between two specific characters in a bitmap font.

**Intent:** Store the horizontal offset applied between a specific first and second glyph pair to improve the visual spacing of rendered text.

**Use-case:** Consumed internally by `FontAsset` during text layout. Individual `Kerning` entries are stored in `FontAsset.Kernings` and applied automatically when the font renders adjacent characters that benefit from tighter or looser spacing.

### ⭐ Constructors
```csharp
public Kerning()
```

### ⭐ Properties
#### Amount
```csharp
public int Amount { get; public set; }
```

Pixel offset applied to the horizontal advance when the `Second` glyph follows `First`.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
#### First
```csharp
public int First { get; public set; }
```

Unicode code-point of the leading character in this kerning pair.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
#### Second
```csharp
public int Second { get; public set; }
```

Unicode code-point of the trailing character in this kerning pair.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \


⚡