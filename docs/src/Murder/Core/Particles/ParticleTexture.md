# ParticleTexture

**Namespace:** Murder.Core.Particles \
**Assembly:** Murder.dll

```csharp
public sealed struct ParticleTexture
```

Describes the texture or primitive shape used to draw individual particles (point, rectangle, circle, asset, or named texture).

**Intent:** Configure the visual representation of a particle.

**Use-case:** Set `Kind` to `Asset` and provide a `Guid` to render a sprite-based particle, or use `Point`, `Rectangle`, or `Circle` for procedurally drawn primitives, or `Texture` for a texture looked up by name. Assign a `ParticleTexture` to `Particle.Texture`; `ParticleRendererSystem` switches on `Kind` every draw call to pick the matching draw path for each live particle.

### ⭐ Constructors

```csharp
public ParticleTexture()
```

The default constructor, leaving `Kind` at `ParticleTextureKind.Point` — the cheapest possible particle visual (a single drawn pixel), useful as a placeholder before an artist assigns real art.

```csharp
public ParticleTexture(Circle circle)
```

Creates a texture that renders each particle as a filled `Circle` primitive, setting `Kind` to `ParticleTextureKind.Circle`.

**Parameters** \
`circle` [Circle](../../../Murder/Core/Geometry/Circle.html) \

```csharp
public ParticleTexture(Rectangle rectangle)
```

Creates a texture that renders each particle as a filled `Rectangle` primitive, setting `Kind` to `ParticleTextureKind.Rectangle`.

**Parameters** \
`rectangle` [Rectangle](../../../Murder/Core/Geometry/Rectangle.html) \

```csharp
public ParticleTexture(Guid asset)
```

Creates a texture that renders each particle as a sprite loaded from the given `SpriteAsset` GUID, setting `Kind` to `ParticleTextureKind.Asset`. This is the usual choice for hand-authored particle art.

**Parameters** \
`asset` [Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \

```csharp
public ParticleTexture(string texture)
```

Creates a texture that renders each particle using a named texture path (resolved at draw time via `Game.Data.FetchTexture`), setting `Kind` to `ParticleTextureKind.Texture`.

**Parameters** \
`texture` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

### ⭐ Properties

#### Asset

```csharp
public readonly Guid Asset;
```

GUID of the sprite asset used when `Kind` is `ParticleTextureKind.Asset`.

**Returns** \
[Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \

#### Circle

```csharp
public readonly Circle Circle;
```

Circle geometry used when `Kind` is `ParticleTextureKind.Circle` or `ParticleTextureKind.CircleOutline`.

**Returns** \
[Circle](../../../Murder/Core/Geometry/Circle.html) \

#### Kind

```csharp
public readonly ParticleTextureKind Kind;
```

Determines which visual representation is used for rendering this particle.

**Returns** \
[ParticleTextureKind](../../../Murder/Core/Particles/ParticleTextureKind.html) \

#### Rectangle

```csharp
public readonly Rectangle Rectangle;
```

Rectangle geometry used when `Kind` is `ParticleTextureKind.Rectangle`.

**Returns** \
[Rectangle](../../../Murder/Core/Geometry/Rectangle.html) \

#### Texture

```csharp
public readonly string Texture;
```

Named texture path used when `Kind` is `ParticleTextureKind.Texture`.

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

⚡
