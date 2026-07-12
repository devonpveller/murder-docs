# TextSettings

**Namespace:** Murder.Core.Graphics \
**Assembly:** Murder.dll

```csharp
public sealed struct TextSettings
```

Layout parameters passed to `TextDataServices.GetOrCreateText()` that influence how a raw string is word-wrapped, independent of the text content itself.

**Intent:** Groups the parameters — scale and maximum line width — that affect word-wrapping, plus a `HiRes` flag threaded through to the resulting `RuntimeTextData`. Two calls with the same text, font, and `MaxWidth` hit the same parsed-text cache entry, so prefer reusing equivalent settings instances rather than constructing new ones needlessly.

**Use-case:** Construct a `TextSettings` and pass it to `TextDataServices.GetOrCreateText()` whenever you need scaled or word-wrapped text; `PixelFont.Draw()` builds one internally from its own `scale`/`maxWidth` parameters.

### ⭐ Constructors

```csharp
public TextSettings()
```

Creates settings with unscaled glyphs, standard resolution, and no wrap width.

### ⭐ Properties

#### HiRes

```csharp
public bool HiRes { get; public set; }
```

Threaded through to the resulting `RuntimeTextData.HiRes`. Not currently consumed by the wrapping or rendering logic itself.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### MaxWidth

```csharp
public int MaxWidth { get; public set; }
```

Maximum line width, in pixels (after applying `Scale`), before text is word-wrapped onto the next line. A value less than or equal to 0 disables wrapping entirely; the default is -1 (unlimited).

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### Scale

```csharp
public Vector2 Scale { get; public set; }
```

Scale applied to the glyphs; used together with `MaxWidth` to compute how much text fits per line before wrapping (a larger scale wraps sooner for the same pixel width). Use `Vector2.One` for native size.

**Returns** \
[Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

⚡
