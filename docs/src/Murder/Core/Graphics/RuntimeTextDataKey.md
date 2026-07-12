# RuntimeTextDataKey

**Namespace:** Murder.Core.Graphics \
**Assembly:** Murder.dll

```csharp
public sealed struct RuntimeTextDataKey : IEquatable<T>
```

Cache key identifying a unique combination of text content, font index, and maximum display width.

**Intent:** Allows `TextDataServices` to store and retrieve pre-parsed `RuntimeTextData` layouts without re-processing identical text configurations.

**Use-case:** Created automatically inside `TextDataServices.GetOrCreateText()`; developers rarely construct this directly.

**Implements:** _[IEquatable\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.IEquatable-1?view=net-7.0)_

### ⭐ Constructors

```csharp
public RuntimeTextDataKey(string Text, int Font, int Width)
```

**Parameters** \
`Text` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
`Font` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`Width` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

### ⭐ Properties

#### Font

```csharp
public int Font { get; public set; }
```

Index of the font used to lay out this text, as registered in the game's font list.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### Text

```csharp
public string Text { get; public set; }
```

The raw text string that was parsed to produce the cached `RuntimeTextData`.

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### Width

```csharp
public int Width { get; public set; }
```

Maximum line width in pixels that was applied during word-wrap layout, or -1 if no width limit was used.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

### ⭐ Methods

#### Equals(RuntimeTextDataKey)

```csharp
public virtual bool Equals(RuntimeTextDataKey other)
```

Returns true if `other` has the same text, font index, and wrap width as this key.

**Parameters** \
`other` [RuntimeTextDataKey](../../../Murder/Core/Graphics/RuntimeTextDataKey.html) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### Equals(Object)

```csharp
public virtual bool Equals(Object obj)
```

Returns true if `obj` is a `RuntimeTextDataKey` with matching text, font, and width values.

**Parameters** \
`obj` [Object](https://learn.microsoft.com/en-us/dotnet/api/System.Object?view=net-7.0) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### GetHashCode()

```csharp
public virtual int GetHashCode()
```

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### ToString()

```csharp
public virtual string ToString()
```

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### Deconstruct(out String&, out Int32&, out Int32&)

```csharp
public void Deconstruct(String& Text, Int32& Font, Int32& Width)
```

**Parameters** \
`Text` [string&](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
`Font` [int&](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`Width` [int&](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

⚡
