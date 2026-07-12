# Batches2D

**Namespace:** Murder.Core.Graphics \
**Assembly:** Murder.dll

```csharp
public class Batches2D
```

A list of all available [Batch2D](../../../Murder/Core/Graphics/Batch2D.html) layers in your [RenderContext](../../../Murder/Core/Graphics/RenderContext.html).
If you extend this class it will automatically show the new constants on the "Target SpriteBatch" in the inspector.
Variables have "BatchId" and "Batch" trimmed for display.
Numbers from 0 to 20 are reserved for Murder internal use.

**Intent:** Centralises the integer identifiers for every built-in render layer so systems and components can reference a layer by a named constant rather than a magic number.

**Use-case:** Extend this class in your game to define additional batch IDs above 20, then reference them in `DrawInfo.Sort` or sprite-component fields to route draw calls to the correct layer.

### ⭐ Constructors

```csharp
public Batches2D()
```

### ⭐ Properties

#### DebugBatchId

```csharp
public static const int DebugBatchId;
```

Batch layer for debug overlays (shapes, text, etc.) drawn on top of everything.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### DebugFxBatchId

```csharp
public static const int DebugFxBatchId;
```

Batch layer for debug visual effects, rendered just below the main debug overlay.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### FloorBatchId

```csharp
public static const int FloorBatchId;
```

Batch layer for floor/ground-level sprites drawn beneath gameplay objects.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### GameplayBatchId

```csharp
public static const int GameplayBatchId;
```

The main gameplay batch layer (ID 0); used for most in-world sprites and entities.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### GameUiBatchId

```csharp
public static const int GameUiBatchId;
```

Batch layer for in-game UI elements that exist in world space (health bars, nameplates, etc.).

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### UiBatchId

```csharp
public static const int UiBatchId;
```

Batch layer for screen-space UI elements that are composited after the game world.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

⚡
