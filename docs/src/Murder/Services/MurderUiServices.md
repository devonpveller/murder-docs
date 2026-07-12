# MurderUiServices

**Namespace:** Murder.Services \
**Assembly:** Murder.dll

```csharp
public static class MurderUiServices
```

Static container for reusable UI configuration data types. It currently declares no methods; it only nests two configuration structs, `BoxUiInfo` and `ButtonInfo`.

**Intent:** Gives higher-level, game-specific UI code (not yet part of the engine's own systems) a shared place to define the visual parameters of common widgets — a text box and a button — without every game reinventing similar structs. As of this writing neither nested struct has any engine-side consumer; they exist as scaffolding for game code (or a future built-in UI system) to build on.

**Use-case:** If your game builds its own dialogue box or button widgets, you can reuse `MurderUiServices.BoxUiInfo`/`MurderUiServices.ButtonInfo` as the parameter type instead of defining an equivalent struct from scratch, keeping the field names consistent with the rest of the engine's UI-adjacent code (`RenderServices.DrawVerticalMenu`, `MenuInfo`, `DrawMenuStyle`).

### ⭐ Nested Types

#### BoxUiInfo

```csharp
public struct BoxUiInfo
```

Visual configuration for a nine-sliced text/dialogue box: which sprite to nine-slice (`NineSliceGuid`), the text and border colors, optional fade values used during transitions (`BoxFade`, `TextFade`), an optional background fade color (`BackgroundFadeColor`), the box's pixel `Width`, extra bottom padding (`ExtraHeight`), and the normalized `TextAlignment` within the box. `WhiteFadeColor` is a computed convenience property (`Color.White * BoxFade`) for tinting overlay elements alongside the box's own fade.

#### ButtonInfo

```csharp
public struct ButtonInfo
```

Visual configuration for a button or group of buttons: the button `Sprite`, the label(s) to show (`ButtonsText`), the text/border colors, an optional `MenuInfo` for when multiple buttons are displayed as a navigable list, and an `IsButtonValid` flag for marking the button's current enabled/valid state.

⚡
