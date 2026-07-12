# Matrix

**Namespace:** Murder.Core.Geometry \
**Assembly:** Murder.dll

```csharp
public sealed struct Matrix : IEquatable<T>
```

Implements a matrix within our engine. It can be converted to other matrix data types.

**Intent:** Murder's 2D transformation matrix, wrapping XNA's `Matrix` for camera and world-to-screen transforms.

**Use-case:** Used primarily by `Camera2D` for world-to-screen coordinate transformations; prefer the helper methods over manipulating matrix elements directly.

**Implements:** _[IEquatable\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.IEquatable-1?view=net-7.0)_

### ⭐ Properties

#### Identity

```csharp
public static Matrix Identity { get; }
```

Just a shorthand for [Matrix.Identity](https://docs.monogame.net/api/Microsoft.Xna.Framework.Matrix.html) for when you don't want to import the whole XNA Framework Matrix Library

**Returns** \
[Matrix](https://docs.monogame.net/api/Microsoft.Xna.Framework.Matrix.html) \

#### M11

```csharp
public float M11;
```

A first row and first column value.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### M12

```csharp
public float M12;
```

A first row and second column value.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### M13

```csharp
public float M13;
```

A first row and third column value.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### M14

```csharp
public float M14;
```

A first row and fourth column value.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### M21

```csharp
public float M21;
```

A second row and first column value.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### M22

```csharp
public float M22;
```

A second row and second column value.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### M23

```csharp
public float M23;
```

A second row and third column value.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### M24

```csharp
public float M24;
```

A second row and fourth column value.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### M31

```csharp
public float M31;
```

A third row and first column value.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### M32

```csharp
public float M32;
```

A third row and second column value.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### M33

```csharp
public float M33;
```

A third row and third column value.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### M34

```csharp
public float M34;
```

A third row and fourth column value.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### M41

```csharp
public float M41;
```

A fourth row and first column value.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### M42

```csharp
public float M42;
```

A fourth row and second column value.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### M43

```csharp
public float M43;
```

A fourth row and third column value.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### M44

```csharp
public float M44;
```

A fourth row and fourth column value.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

### ⭐ Methods

#### ToXnaMatrix()

```csharp
public Matrix ToXnaMatrix()
```

Converts this matrix into a MonoGame `Matrix` with the same element values, for use in APIs (e.g. `SpriteBatch` transforms) that require XNA's own type.

**Returns** \
[Matrix](https://docs.monogame.net/api/Microsoft.Xna.Framework.Matrix.html) \

#### Equals(Matrix)

```csharp
public bool Equals(Matrix other)
```

Compares whether `other` has the same matrix elements as this matrix.

**Parameters** \
`other` [Matrix](../../../Murder/Core/Geometry/Matrix.html) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

⚡
