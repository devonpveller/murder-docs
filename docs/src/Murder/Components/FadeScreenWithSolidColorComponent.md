# FadeScreenWithSolidColorComponent

**Namespace:** Murder.Components \
**Assembly:** Murder.dll

```csharp
public sealed struct FadeScreenWithSolidColorComponent : IComponent
```

Drives a simple full-screen solid-color fade managed by `FadeScreenWithSolidColorSystem`.

**Implements:** _[IComponent](../../Bang/Components/IComponent.html)_

**Intent:** Provides a lightweight alternative to `FadeScreenComponent` when only a plain colored overlay fade is needed.

**Use-case:** Add to the world entity when you need a fast solid-color fade-in or fade-out without custom textures or buffering.

### ⭐ Constructors
```csharp
public FadeScreenWithSolidColorComponent(Color color, FadeType fade, float duration)
```

**Parameters** \
`color` [Color](../../Murder/Core/Graphics/Color.html) \
`fade` [FadeType](../../Murder/Components/FadeType.html) \
`duration` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

### ⭐ Properties
#### Color
```csharp
public readonly Color Color;
```

Color of the solid overlay used for the fade effect.

**Returns** \
[Color](../../Murder/Core/Graphics/Color.html) \
#### Duration
```csharp
public readonly float Duration;
```

Duration of the fade effect in seconds.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
#### FadeType
```csharp
public readonly FadeType FadeType;
```

The direction of the fade (in or out).

**Returns** \
[FadeType](../../Murder/Components/FadeType.html) \


⚡