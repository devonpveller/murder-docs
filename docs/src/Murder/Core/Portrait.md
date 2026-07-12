# Portrait

**Namespace:** Murder.Core \
**Assembly:** Murder.dll

```csharp
public readonly struct Portrait : IEquatable<Portrait>
```

A lightweight reference to a single animation within a `SpriteAsset`, used to pick which portrait image to show for a character.

**Intent:** Combines a sprite sheet's asset GUID with the name of one of its animations (e.g. "Idle", "Happy", "Angry") so a character or dialog line can point at a specific expression without embedding any texture data itself.

**Use-case:** Assign a `Portrait` on a `Character`/`CharacterAsset`, `SpeakerAsset`, or dialog `Line` to control which sprite and animation are shown when a character speaks. Dialog/UI rendering code queries `HasImage`/`GetSize` before drawing it.

**Implements:** _[IEquatable\<Portrait\>](https://learn.microsoft.com/en-us/dotnet/api/System.IEquatable-1?view=net-7.0)_

### ⭐ Constructors

```csharp
public Portrait()
```

Creates an empty portrait with no sprite and no animation. Used as the default/blank state by the editor and serializer.

```csharp
public Portrait(Guid aseprite, string animationId)
```

Creates a portrait pointing at the given sprite asset and one of its animations.

**Parameters** \
`aseprite` [Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \
`animationId` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

### ⭐ Properties

#### AnimationId

```csharp
public readonly string AnimationId { get; init; }
```

The name of the animation within `Sprite` to display as the portrait, e.g. "Idle" or "Talk".

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### HasImage

```csharp
public bool HasImage { get; }
```

Whether `Sprite` resolves to an actual loaded `SpriteAsset` and that asset actually contains an animation named `AnimationId`. Unlike `HasValue`, this performs a real asset lookup, so it also catches stale/broken references (e.g. after an animation was renamed or removed in the sprite editor).

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### HasValue

```csharp
public bool HasValue { get; }
```

Whether this portrait references a sprite asset at all (`Sprite` is not `Guid.Empty`). Does not verify that the referenced asset or animation actually exist; see `HasImage` for that.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### Sprite

```csharp
[GameAssetId(typeof(SpriteAsset))]
public readonly Guid Sprite { get; init; }
```

The asset GUID of the `SpriteAsset` (aseprite) that contains the portrait's animation.

**Returns** \
[Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \

### ⭐ Methods

#### GetSize()

```csharp
public Point GetSize()
```

Returns the pixel dimensions of the referenced `SpriteAsset`, or `Point.Zero` if `Sprite` does not resolve to a loaded asset. Used by UI/dialog rendering code to lay out portrait art without hardcoding its size.

**Returns** \
[Point](../../Murder/Core/Geometry/Point.html) \

#### Equals(Portrait)

```csharp
public bool Equals(Portrait other)
```

Two portraits are equal when they reference the same sprite asset and the same animation id.

**Parameters** \
`other` [Portrait](../../Murder/Core/Portrait.html) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

⚡
