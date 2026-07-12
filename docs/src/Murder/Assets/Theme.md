# Theme

**Namespace:** Murder.Assets \
**Assembly:** Murder.dll

```csharp
public class Theme
```

Defines the color palette used by the Murder editor UI and in-game UI systems.

**Intent:** Provide a single, serializable set of named RGBA color slots that the editor and UI renderer read from, allowing visual themes to be swapped or customised without code changes.

**Use-case:** Reference `Game.Profile.Theme` to obtain any named color (e.g. `Theme.Accent`, `Theme.Red`) when drawing custom editor windows or in-game UI elements. Override the default `Theme` instance in `GameProfile` to ship a branded color scheme.

### ⭐ Constructors

```csharp
public Theme()
```

### ⭐ Properties

#### Accent

```csharp
public Vector4 Accent;
```

Primary accent color used for highlighted or interactive UI elements.

**Returns** \
[Vector4](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector4?view=net-7.0) \

#### Bg

```csharp
public Vector4 Bg;
```

Base background color for panels and windows.

**Returns** \
[Vector4](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector4?view=net-7.0) \

#### BgFaded

```csharp
public Vector4 BgFaded;
```

Slightly lighter background color used for secondary panels or alternating rows.

**Returns** \
[Vector4](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector4?view=net-7.0) \

#### BgHeader

```csharp
public Vector4 BgHeader;
```

Background color for header bars and title strips (e.g. window titles, section headers).

**Returns** \
[Vector4](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector4?view=net-7.0) \

#### Faded

```csharp
public Vector4 Faded;
```

Muted foreground color used for disabled or less important text and icons.

**Returns** \
[Vector4](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector4?view=net-7.0) \

#### Foreground

```csharp
public Vector4 Foreground;
```

Primary foreground color used for standard text and icons.

**Returns** \
[Vector4](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector4?view=net-7.0) \

#### GenericAsset

```csharp
public Vector4 GenericAsset;
```

Color used to tint generic asset entries in the editor asset browser.

**Returns** \
[Vector4](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector4?view=net-7.0) \

#### Green

```csharp
public Vector4 Green;
```

Green semantic color used for success states, positive values, or additive indicators.

**Returns** \
[Vector4](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector4?view=net-7.0) \

#### HighAccent

```csharp
public Vector4 HighAccent;
```

High-contrast accent color for strongly highlighted or selected UI elements.

**Returns** \
[Vector4](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector4?view=net-7.0) \

#### Red

```csharp
public Vector4 Red;
```

Red semantic color used for error states, destructive actions, or negative values.

**Returns** \
[Vector4](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector4?view=net-7.0) \

#### RedFaded

```csharp
public Vector4 RedFaded;
```

Muted red color used for subdued error or warning backgrounds.

**Returns** \
[Vector4](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector4?view=net-7.0) \

#### Selected

```csharp
public Vector4 Selected;
```

Background color applied to the currently selected item in a list, tree, or menu.

**Returns** \
[Vector4](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector4?view=net-7.0) \

#### Warning

```csharp
public Vector4 Warning;
```

Orange/amber color used to draw attention to non-critical warnings or cautions.

**Returns** \
[Vector4](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector4?view=net-7.0) \

#### White

```csharp
public Vector4 White;
```

Near-white color used for primary highlighted text or maximum-brightness UI elements.

**Returns** \
[Vector4](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector4?view=net-7.0) \

#### Yellow

```csharp
public Vector4 Yellow;
```

Yellow color used for informational labels, special indicators, or gold-tier values.

**Returns** \
[Vector4](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector4?view=net-7.0) \

#### YellowFaded

```csharp
public Vector4 YellowFaded;
```

Muted yellow color used for subdued informational backgrounds paired with `Yellow` foreground text.

**Returns** \
[Vector4](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector4?view=net-7.0) \

⚡
