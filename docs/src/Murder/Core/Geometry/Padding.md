# Padding

**Namespace:** Murder.Core.Geometry \
**Assembly:** Murder.dll

```csharp
public sealed struct Padding
```

Stores top, right, bottom, and left integer padding or margin values.

**Intent:** Represent uniform or asymmetric inset/outset values for layout and UI calculations.

**Use-case:** Pass a `Padding` to UI drawing helpers to add inner spacing around a region, or use it when shrinking/expanding `IntRectangle` bounds by different amounts on each side.

### ⭐ Constructors

```csharp
public Padding(int border)
```

**Parameters** \
`border` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

```csharp
public Padding(int top, int left, int right, int bottom)
```

**Parameters** \
`top` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`left` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`right` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`bottom` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

### ⭐ Properties

#### Bottom

```csharp
public int Bottom;
```

The bottom padding value.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### Height

```csharp
public int Height { get; }
```

The total vertical padding (`Top + Bottom`).

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### Left

```csharp
public int Left;
```

The left padding value.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### Right

```csharp
public int Right;
```

The right padding value.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### Top

```csharp
public int Top;
```

The top padding value.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### Width

```csharp
public int Width { get; }
```

The total horizontal padding (`Left + Right`).

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

⚡
