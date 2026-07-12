# TextureComponent

**Namespace:** Murder.Components \
**Assembly:** Murder.dll

```csharp
public sealed struct TextureComponent : IComponent
```

Holds a raw `Texture2D` to be rendered on an entity at runtime, bypassing the atlas/asset pipeline.

**Intent:** Render an already-loaded GPU texture directly on an entity, without going through the sprite/atlas asset pipeline used by sprite components.

**Use-case:** Use when a texture is created procedurally at runtime (e.g. a render-target or a captured screenshot) and needs to be displayed on a world entity. Art shipped as game assets should use a sprite component instead.

**Implements:** _[IComponent](../../Bang/Components/IComponent.html)_

### ⭐ Constructors

```csharp
public TextureComponent(Texture2D texture, int targetSpriteBatch)
```

Creates a component that draws `texture` into the given sprite batch layer, with `AutoDispose` defaulting to `true`.

**Parameters** \
`texture` [Texture2D](https://docs.monogame.net/api/Microsoft.Xna.Framework.Graphics.Texture2D.html) \
`targetSpriteBatch` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

### ⭐ Properties

#### AutoDispose

```csharp
public readonly bool AutoDispose;
```

When `true` (the default), `Texture` is disposed automatically once this component is removed from the entity or the render system exits. Set to `false` if the texture is owned/disposed elsewhere (e.g. a shared render target reused across multiple entities).

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### TargetSpriteBatch

```csharp
public readonly int TargetSpriteBatch;
```

Sprite batch layer used when rendering this texture; defaults to the gameplay batch.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### Texture

```csharp
public readonly Texture2D Texture;
```

The raw GPU texture drawn on the entity every frame, at its global position.

**Returns** \
[Texture2D](https://docs.monogame.net/api/Microsoft.Xna.Framework.Graphics.Texture2D.html) \

⚡
