# PaletteColorAttribute

**Namespace:** Murder.Utilities.Attributes \
**Assembly:** Murder.dll

```csharp
public class PaletteColorAttribute : Attribute
```

Marks a `Color` field as a palette color reference, so the editor shows a palette picker alongside the regular color picker.

**Intent:** Lets a component/asset field snap to an established color in the game's palette instead of always picking an arbitrary free-form RGBA color.

**Use-case:** Apply to a [Color](../../../Murder/Core/Graphics/Color.html) field, e.g. `DrawRectangleComponent`'s fill color or the various colors on `ButtonStyle`/`DrawMenuStyle`. The editor's `CoreColorField.DrawPalettePicker` detects the attribute and, next to the RGBA sliders, shows a combo box listing the colors in `Game.Data.CurrentPalette`, letting designers pick a palette entry with one click.

**Implements:** _[Attribute](https://learn.microsoft.com/en-us/dotnet/api/System.Attribute?view=net-7.0)_

### ⭐ Constructors

```csharp
public PaletteColorAttribute()
```

Creates the attribute. Carries no data; its mere presence on a field is what the editor checks for.

### ⭐ Properties

#### TypeId

```csharp
public virtual Object TypeId { get; }
```

Unique object identity for this attribute type, inherited from `Attribute`.

**Returns** \
[Object](https://learn.microsoft.com/en-us/dotnet/api/System.Object?view=net-7.0) \

⚡
