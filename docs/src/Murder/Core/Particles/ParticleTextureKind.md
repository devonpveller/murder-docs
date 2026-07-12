# ParticleTextureKind

**Namespace:** Murder.Core.Particles \
**Assembly:** Murder.dll

```csharp
public sealed enum ParticleTextureKind : Enum, IComparable, ISpanFormattable, IFormattable, IConvertible
```

Specifies how an individual particle's visual is sourced.

**Intent:** Select the rendering mode for a `ParticleTexture`.

**Implements:** _[Enum](https://learn.microsoft.com/en-us/dotnet/api/System.Enum?view=net-7.0), [IComparable](https://learn.microsoft.com/en-us/dotnet/api/System.IComparable?view=net-7.0), [ISpanFormattable](https://learn.microsoft.com/en-us/dotnet/api/System.ISpanFormattable?view=net-7.0), [IFormattable](https://learn.microsoft.com/en-us/dotnet/api/System.IFormattable?view=net-7.0), [IConvertible](https://learn.microsoft.com/en-us/dotnet/api/System.IConvertible?view=net-7.0)_

### ⭐ Properties

#### Asset

```csharp
public static const ParticleTextureKind Asset;
```

Render using a sprite loaded from a `ParticleSystemAsset` GUID.

**Returns** \
[ParticleTextureKind](../../../Murder/Core/Particles/ParticleTextureKind.html) \

#### Circle

```csharp
public static const ParticleTextureKind Circle;
```

Render as a filled circle primitive.

**Returns** \
[ParticleTextureKind](../../../Murder/Core/Particles/ParticleTextureKind.html) \

#### CircleOutline

```csharp
public static const ParticleTextureKind CircleOutline;
```

Render as a circle outline (stroke only).

**Returns** \
[ParticleTextureKind](../../../Murder/Core/Particles/ParticleTextureKind.html) \

#### Point

```csharp
public static const ParticleTextureKind Point;
```

Render as a single pixel point.

**Returns** \
[ParticleTextureKind](../../../Murder/Core/Particles/ParticleTextureKind.html) \

#### Rectangle

```csharp
public static const ParticleTextureKind Rectangle;
```

Render as a filled rectangle primitive.

**Returns** \
[ParticleTextureKind](../../../Murder/Core/Particles/ParticleTextureKind.html) \

#### Texture

```csharp
public static const ParticleTextureKind Texture;
```

Render using a named texture path.

**Returns** \
[ParticleTextureKind](../../../Murder/Core/Particles/ParticleTextureKind.html) \

⚡
