# InputHelpers

**Namespace:** Murder.Utilities \
**Assembly:** Murder.dll

```csharp
public static class InputHelpers
```

Utilities for text fitting, line counting, and D-pad slot label formatting used by input display systems.

**Intent:** Provides helpers for measuring and wrapping text within a pixel width, and for converting numeric input slot indices to display strings.

**Use-case:** Use `FitToWidth` and `GetAmountOfLines` for dialogue text layout, and `IntToDPad` to render controller button labels.

### ⭐ Methods
#### FitToWidth(ReadOnlySpan`1&, int)
```csharp
public bool FitToWidth(ReadOnlySpan`1& text, int width)
```

Truncates or word-wraps the text span to fit within the given pixel width; returns `true` if the text was modified.

**Parameters** \
`text` [ReadOnlySpan\<T\>&](https://learn.microsoft.com/en-us/dotnet/api/System.ReadOnlySpan-1?view=net-7.0) \
`width` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### GetAmountOfLines(ReadOnlySpan<T>, int)
```csharp
public int GetAmountOfLines(ReadOnlySpan<T> text, int width)
```

Returns the number of display lines the text would occupy when rendered at the given pixel width.

**Parameters** \
`text` [ReadOnlySpan\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.ReadOnlySpan-1?view=net-7.0) \
`width` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### IntToDPad(int)
```csharp
public string IntToDPad(int slot)
```

Converts a numeric input slot index to its corresponding D-pad button label string.

**Parameters** \
`slot` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### Clamp(int)
```csharp
public void Clamp(int length)
```

Clamps the current input or text value to the given maximum character length.

**Parameters** \
`length` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \



⚡