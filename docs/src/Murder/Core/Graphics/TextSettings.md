# TextSettings

**Namespace:** Murder.Core.Graphics \
**Assembly:** Murder.dll

```csharp
public sealed struct TextSettings
```

Configuration options that control how raw text is parsed and laid out into a `RuntimeTextData`.

**Intent:** Groups the display parameters — render scale, hi-res mode, and maximum line width — that influence text layout independently of the text content itself.

**Use-case:** Construct a `TextSettings` and pass it to `TextDataServices.GetOrCreateText()` when you need scaled, hi-res, or word-wrapped text.

### ⭐ Constructors
```csharp
public TextSettings()
```

### ⭐ Properties
#### HiRes
```csharp
public bool HiRes { get; public set; }
```

When true, renders the font at double resolution for high-DPI or zoomed-in displays.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
#### MaxWidth
```csharp
public int MaxWidth { get; public set; }
```

Maximum pixel width before text is word-wrapped onto the next line; set to -1 for unlimited width.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
#### Scale
```csharp
public Vector2 Scale { get; public set; }
```

Uniform scale applied to the font when measuring and rendering; use `Vector2.One` for native size.

**Returns** \
[Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \


⚡