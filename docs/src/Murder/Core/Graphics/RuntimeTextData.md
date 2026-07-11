# RuntimeTextData

**Namespace:** Murder.Core.Graphics \
**Assembly:** Murder.dll

```csharp
public sealed struct RuntimeTextData
```

This has runtime information about a text which is displayed in screen.

**Intent:** Holds the parsed, layout-ready representation of a text string along with optional per-character property overrides, used directly by `PixelFont.Draw()`.

**Use-case:** Obtain an instance from `TextDataServices.GetOrCreateText()` and pass it to `PixelFont.Draw()` each frame; the data is cached automatically to avoid re-parsing.

### ⭐ Constructors
```csharp
public RuntimeTextData()
```

```csharp
public RuntimeTextData(string text, ImmutableDictionary<TKey, TValue> letters)
```

**Parameters** \
`text` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
`letters` [ImmutableDictionary\<TKey, TValue\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableDictionary-2?view=net-7.0) \

```csharp
public RuntimeTextData(string text)
```

**Parameters** \
`text` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

### ⭐ Properties
#### Empty
```csharp
public bool Empty { get; }
```

Returns true when the text string is null or empty, indicating there is nothing to render.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
#### Font
```csharp
public int Font { get; public set; }
```

Index of the font used to calculate the runtime text data.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
#### HiRes
```csharp
public bool HiRes { get; public set; }
```

Whether this is high resolution.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
#### Length
```csharp
public int Length { get; }
```

Total number of characters in the text string, used by typewriter systems to control the reveal progress.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
#### Text
```csharp
public readonly string Text;
```

The raw text string after markup pre-processing, used as the source for all glyph lookups.

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
### ⭐ Methods
#### TryGetLetterProperty(int)
```csharp
public T? TryGetLetterProperty(int index)
```

Returns the `RuntimeLetterProperties` for the character at `index` if one was set by the markup parser, or null if no override exists.

**Parameters** \
`index` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

**Returns** \
[T?](https://learn.microsoft.com/en-us/dotnet/api/System.Nullable-1?view=net-7.0) \



⚡