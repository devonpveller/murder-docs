# TintComponent

**Namespace:** Murder.Components.Graphics \
**Assembly:** Murder.dll

```csharp
public sealed struct TintComponent : IComponent, IEquatable<T>
```

Applies a solid color tint to the entity's entire sprite, blending the tint color multiplicatively with the original pixel colors.

**Intent:** Colorize or recolor a sprite at runtime without modifying the source asset.

**Use-case:** Add with a chosen `TintColor` to highlight an entity (e.g. a red tint on damage), and remove the component to restore the original appearance.

**Implements:** _[IComponent](../../../Bang/Components/IComponent.html), [IEquatable\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.IEquatable-1?view=net-7.0)_

### ⭐ Constructors
```csharp
public TintComponent(Color TintColor)
```

**Parameters** \
`TintColor` [Color](../../../Murder/Core/Graphics/Color.html) \

### ⭐ Properties
#### TintColor
```csharp
public Color TintColor { get; public set; }
```

The color multiplied with every pixel of the sprite to produce the tinted result.

**Returns** \
[Color](../../../Murder/Core/Graphics/Color.html) \
### ⭐ Methods
#### Equals(TintComponent)
```csharp
public virtual bool Equals(TintComponent other)
```

Returns `true` if `other` has the same `TintColor` as this instance.

**Parameters** \
`other` [TintComponent](../../../Murder/Components/Graphics/TintComponent.html) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### Equals(Object)
```csharp
public virtual bool Equals(Object obj)
```

Returns `true` if `obj` is a `TintComponent` with the same `TintColor`.

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

#### Deconstruct(out Color&)
```csharp
public void Deconstruct(Color& TintColor)
```

**Parameters** \
`TintColor` [Color&](../../../Murder/Core/Graphics/Color.html) \



⚡