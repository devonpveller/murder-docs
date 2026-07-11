# TextureComponent

**Namespace:** Murder.Components \
**Assembly:** Murder.dll

```csharp
public sealed struct TextureComponent : IComponent
```

Holds a raw `Texture2D` to be rendered on an entity at runtime, bypassing the atlas/asset pipeline.

**Intent:** Render a dynamically generated or externally loaded texture on an entity.

**Use-case:** Use when a texture is created procedurally at runtime (e.g. a render-target or a captured screenshot) and needs to be displayed on a world entity.

**Implements:** _[IComponent](../../Bang/Components/IComponent.html)_

### ⭐ Constructors
```csharp
public TextureComponent(Texture2D texture, int targetSpriteBatch)
```

**Parameters** \
`texture` [Texture2D](https://docs.monogame.net/api/Microsoft.Xna.Framework.Graphics.Texture2D.html) \
`targetSpriteBatch` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

### ⭐ Properties
#### AutoDispose
```csharp
public readonly bool AutoDispose;
```

When true, the `Texture2D` is automatically disposed when the component is removed or the entity is destroyed.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
#### TargetSpriteBatch
```csharp
public readonly int TargetSpriteBatch;
```

Sprite batch layer used when rendering this texture.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
#### Texture
```csharp
public readonly Texture2D Texture;
```

The raw GPU texture to be drawn on the entity.

**Returns** \
[Texture2D](https://docs.monogame.net/api/Microsoft.Xna.Framework.Graphics.Texture2D.html) \


⚡