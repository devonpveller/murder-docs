# SimpleButton

**Namespace:** Murder.Core.Ui \
**Assembly:** Murder.dll

```csharp
public class SimpleButton
```

A lightweight UI button that tracks hover, press, and disabled states and renders the appropriate sprite frame from a sprite asset.

**Intent:** Minimal clickable button for in-game UI menus that doesn't require a full UI framework.

**Use-case:** Instantiate with a sprite asset GUID and a screen rectangle, call `Update` each frame with the cursor position and click state, and call `Draw` to render it.

### ⭐ Constructors
```csharp
public SimpleButton(Guid images, Rectangle rectangle)
```

Creates a button with the given sprite asset and screen rectangle in the default `Normal` state.

**Parameters** \
`images` [Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \
`rectangle` [Rectangle](../../../Murder/Core/Geometry/Rectangle.html) \

```csharp
public SimpleButton(Guid images, ButtonState state, Rectangle rectangle)
```

Creates a button with the given sprite asset, initial state, and screen rectangle.

**Parameters** \
`images` [Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \
`state` [ButtonState](../../../Murder/Core/Ui/ButtonState.html) \
`rectangle` [Rectangle](../../../Murder/Core/Geometry/Rectangle.html) \

### ⭐ Properties
#### Images
```csharp
public Guid Images;
```

The GUID of the sprite asset used to draw the button in each of its states.

**Returns** \
[Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \
#### Rectangle
```csharp
public Rectangle Rectangle;
```

The screen-space rectangle that defines the button's hit area and render bounds.

**Returns** \
[Rectangle](../../../Murder/Core/Geometry/Rectangle.html) \
#### State
```csharp
public ButtonState State;
```

The current interaction state of the button (Normal, Hover, Down, or Disabled).

**Returns** \
[ButtonState](../../../Murder/Core/Ui/ButtonState.html) \
### ⭐ Methods
#### Draw(Batch2D, DrawInfo)
```csharp
public void Draw(Batch2D batch, DrawInfo drawInfo)
```

Draws the button sprite corresponding to the current `State` to `batch`.

**Parameters** \
`batch` [Batch2D](../../../Murder/Core/Graphics/Batch2D.html) \
`drawInfo` [DrawInfo](../../../Murder/Core/Graphics/DrawInfo.html) \

#### Update(Point, bool, bool, Action)
```csharp
public void Update(Point cursorPosition, bool cursorClicked, bool cursorDown, Action action)
```

Updates the button's `State` based on cursor input. Invokes `action` when the button is clicked (cursor released over it).

**Parameters** \
`cursorPosition` [Point](../../../Murder/Core/Geometry/Point.html) \
`cursorClicked` [bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
`cursorDown` [bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
`action` [Action](https://learn.microsoft.com/en-us/dotnet/api/System.Action?view=net-7.0) \

#### UpdatePosition(Rectangle)
```csharp
public void UpdatePosition(Rectangle rectangle)
```

Updates the button's hit area and render bounds to the new `rectangle`.

**Parameters** \
`rectangle` [Rectangle](../../../Murder/Core/Geometry/Rectangle.html) \



⚡