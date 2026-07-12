# BoxUiInfo

**Namespace:** Murder.Services \
**Assembly:** Murder.dll

```csharp
public struct BoxUiInfo
```

Style/layout data for a nine-slice UI box with a text label, such as a dialogue box or tooltip panel. Declared as a nested type of [MurderUiServices](../../Murder/Services/MurderUiServices.html).

**Intent:** Bundles the nine-slice art reference, colors, sizing, and fade state a generic "box with text in it" UI element needs, so box-drawing helpers in `MurderUiServices` can take one parameter instead of half a dozen.

**Use-case:** Configure a `BoxUiInfo` (often from editor-exposed fields on a UI style asset) and pass it to the box-drawing routines in `MurderUiServices` to render dialogue boxes, tooltips, or similar panel UI, including fade-in/fade-out transitions via `BoxFade`/`TextFade`/`BackgroundFadeColor`.

### ⭐ Constructors

```csharp
public BoxUiInfo()
```

Creates a `BoxUiInfo` with default optional values: full opacity (`BoxFade`/`TextFade` = `1`), no background fade color, a default `Width` of `160`, an `ExtraHeight` of `5`, and text centered horizontally at the top (`TextAlignment` = `(0.5, 0)`). The required fields (`NineSliceGuid`, `TextColor`, `BorderColor`) have no default and must be set explicitly.

### ⭐ Properties

#### BackgroundFadeColor

```csharp
public Color? BackgroundFadeColor { get; init; }
```

Optional color the box's background fades to/from during a transition; `null` means no background fade color override is applied.

**Returns** \
[Color?](../../Murder/Core/Graphics/Color.html) \

#### BorderColor

```csharp
public Color BorderColor { get; init; }
```

Color of the box's border/outline.

**Returns** \
[Color](../../Murder/Core/Graphics/Color.html) \

#### BoxFade

```csharp
public float BoxFade { get; init; }
```

Fade applied to the box itself when transitioning in/out. Defaults to `1` (fully opaque). Also drives `WhiteFadeColor`.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### ExtraHeight

```csharp
public int ExtraHeight { get; init; }
```

Extra pixel height added after the text when the box is drawn, giving the label room to breathe or accommodating padding/decorations below it. Defaults to `5`.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### NineSliceGuid

```csharp
public Guid NineSliceGuid { get; init; }
```

The GUID of the nine-slice sprite asset used to draw the box's resizable background/border art.

**Returns** \
[Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \

#### TextAlignment

```csharp
public Vector2 TextAlignment { get; init; }
```

Normalized alignment of the text within the box, e.g. the default `(0.5, 0)` centers it horizontally and anchors it to the top.

**Returns** \
[Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

#### TextColor

```csharp
public Color TextColor { get; init; }
```

Color of the text drawn inside the box.

**Returns** \
[Color](../../Murder/Core/Graphics/Color.html) \

#### TextFade

```csharp
public float TextFade { get; init; }
```

Fade applied specifically to the text when transitioning, independently of `BoxFade` — used when only the text should fade (e.g. text appearing after the box has already faded in). Defaults to `1`.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### WhiteFadeColor

```csharp
public readonly Color WhiteFadeColor => Color.White * BoxFade;
```

Computed convenience value: white tinted by the current `BoxFade`, handy for tinting overlay draws that should fade in lockstep with the box.

**Returns** \
[Color](../../Murder/Core/Graphics/Color.html) \

#### Width

```csharp
public int Width { get; init; }
```

The box's width in pixels. Defaults to `160`.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

⚡
