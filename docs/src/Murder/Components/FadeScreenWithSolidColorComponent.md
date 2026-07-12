# FadeScreenWithSolidColorComponent

**Namespace:** Murder.Components \
**Assembly:** Murder.dll

```csharp
public sealed struct FadeScreenWithSolidColorComponent : IComponent
```

Drives a simple full-screen solid-color fade, watched and rendered by `FadeScreenWithSolidColorSystem`.

**Implements:** _[IComponent](../../Bang/Components/IComponent.html)_

**Intent:** Provides a lightweight, self-contained alternative to `FadeScreenComponent` (which has no built-in consuming system) when only a plain colored overlay fade is needed — this one is actually rendered by an engine-provided system. Unlike `FadeScreenComponent`, this is not `[Unique]`; `FadeScreenWithSolidColorSystem` reacts to it being added or changed and, if more than one instance exists in the same frame, prefers the one fading `Out`.

**Use-case:** Add to any entity (commonly the world entity) when you need a fast solid-color fade-in or fade-out without custom textures or buffering; the system draws a rectangle covering `render.Camera.SafeBounds` at `Sort`/`BatchId`, interpolating alpha from `Game.NowUnscaled` over `Duration` and writing the result to `RenderContext.ScreenFade`.

### ⭐ Constructors

```csharp
public FadeScreenWithSolidColorComponent(Color color, FadeType fade, float duration)
```

Creates the component with the default sort order (`0.05`) and the default UI batch as the target.

**Parameters** \
`color` [Color](../../Murder/Core/Graphics/Color.html) \
`fade` [FadeType](../../Murder/Components/FadeType.html) \
`duration` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

```csharp
public FadeScreenWithSolidColorComponent(Color color, FadeType fade, float duration, float sort)
```

Creates the component with an explicit sort order, keeping the default UI batch as the target.

**Parameters** \
`color` [Color](../../Murder/Core/Graphics/Color.html) \
`fade` [FadeType](../../Murder/Components/FadeType.html) \
`duration` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`sort` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

```csharp
public FadeScreenWithSolidColorComponent(int batchId, Color color, FadeType fade, float duration, float sort)
```

Creates the component with an explicit target sprite batch and sort order, for fades that should render into a specific batch other than the UI batch (e.g. a gameplay-space fade).

**Parameters** \
`batchId` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`color` [Color](../../Murder/Core/Graphics/Color.html) \
`fade` [FadeType](../../Murder/Components/FadeType.html) \
`duration` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`sort` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

### ⭐ Properties

#### BatchId

```csharp
public readonly int BatchId;
```

Index of the sprite batch that the fade overlay rectangle is drawn into; defaults to `Batches2D.UiBatchId`. When this equals `Batches2D.GameUiBatchId`, the system draws over `render.Camera.SafeBounds` instead of a screen-space rectangle.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

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

The direction of the fade (`In` or `Out`; `FadeScreenWithSolidColorSystem` only reacts to these two values).

**Returns** \
[FadeType](../../Murder/Components/FadeType.html) \

#### Sort

```csharp
public readonly float Sort;
```

Sort order for the fade overlay within its render batch; defaults to `0.05`.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

⚡
