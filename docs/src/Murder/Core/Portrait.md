# Portrait

**Namespace:** Murder.Core \
**Assembly:** Murder.dll

```csharp
public sealed struct Portrait : IEquatable<T>
```

A reference to a character portrait, combining an aseprite sprite asset GUID with the name of the animation to display.

**Intent:** Lightweight value type that points to a specific animation frame within a sprite sheet used for character portraits in dialogue.

**Use-case:** Assign a `Portrait` to a dialogue line or character asset to control which sprite and animation are shown when a character speaks.

**Implements:** _[IEquatable\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.IEquatable-1?view=net-7.0)_

### ⭐ Constructors
```csharp
public Portrait()
```

Creates an empty portrait with no sprite and no animation.

```csharp
public Portrait(Guid aseprite, string animationId)
```

Creates a portrait referencing the given sprite asset and animation name.

**Parameters** \
`aseprite` [Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \
`animationId` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

### ⭐ Properties
#### AnimationId
```csharp
public readonly string AnimationId;
```

The name of the animation within the sprite sheet to use as the portrait image.

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
#### HasImage
```csharp
public bool HasImage { get; }
```

Returns `true` when both a sprite and a non-empty animation ID are set.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
#### HasValue
```csharp
public bool HasValue { get; }
```

Returns `true` when this portrait references a valid (non-empty) sprite GUID.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
#### Sprite
```csharp
public readonly Guid Sprite;
```

The GUID of the aseprite sprite asset used as the portrait image.

**Returns** \
[Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \
### ⭐ Methods
#### WithAnimationId(string)
```csharp
public Portrait WithAnimationId(string animationId)
```

Returns a copy of this portrait with the animation ID replaced by `animationId`.

**Parameters** \
`animationId` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

**Returns** \
[Portrait](../../Murder/Core/Portrait.html) \

#### Equals(Portrait)
```csharp
public virtual bool Equals(Portrait other)
```

**Parameters** \
`other` [Portrait](../../Murder/Core/Portrait.html) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \



⚡