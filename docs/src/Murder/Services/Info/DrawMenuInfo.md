# DrawMenuInfo

**Namespace:** Murder.Services.Info \
**Assembly:** Murder.dll

```csharp
public sealed struct DrawMenuInfo
```

Carries draw-state data for a menu render pass, including selector position history for smooth animation.

**Intent:** Passes layout and animation state to the menu drawing routine.

**Use-case:** Created internally by `MurderUiServices` during menu rendering; consumed by menu draw calls to position the animated selection cursor.

### ⭐ Constructors
```csharp
public DrawMenuInfo()
```

Creates a `DrawMenuInfo` with default zeroed values.

### ⭐ Properties
#### MaximumSelectionWidth
```csharp
public int MaximumSelectionWidth { get; public set; }
```

The maximum pixel width of any selectable menu item, used to size the selector indicator.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
#### PreviousSelectorPosition
```csharp
public Vector2 PreviousSelectorPosition { get; public set; }
```

The selector's world position during the previous frame, used for interpolation.

**Returns** \
[Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
#### SelectorEasedPosition
```csharp
public Vector2 SelectorEasedPosition { get; public set; }
```

The smoothly-interpolated current position of the selection cursor.

**Returns** \
[Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
#### SelectorPosition
```csharp
public Vector2 SelectorPosition { get; public set; }
```

The target pixel position of the selection cursor for the current frame.

**Returns** \
[Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \


⚡