# BatchPreviewState

**Namespace:** Murder.Core.Graphics \
**Assembly:** Murder.dll

```csharp
sealed enum BatchPreviewState : Enum, IComparable, ISpanFormattable, IFormattable, IConvertible
```

Editor-only enum that selects which intermediate render target is displayed in the editor's batch-preview overlay.

**Intent:** Lets artists and engineers inspect each stage of the `RenderContext` pipeline (floor, gameplay, UI, lights, etc.) independently during development.

**Use-case:** Set `RenderContext.PreviewState` in the editor to the desired `BatchPreviewState` value to isolate a specific render step for visual debugging.

**Implements:** _[Enum](https://learn.microsoft.com/en-us/dotnet/api/System.Enum?view=net-7.0), [IComparable](https://learn.microsoft.com/en-us/dotnet/api/System.IComparable?view=net-7.0), [ISpanFormattable](https://learn.microsoft.com/en-us/dotnet/api/System.ISpanFormattable?view=net-7.0), [IFormattable](https://learn.microsoft.com/en-us/dotnet/api/System.IFormattable?view=net-7.0), [IConvertible](https://learn.microsoft.com/en-us/dotnet/api/System.IConvertible?view=net-7.0)_

### ⭐ Properties

#### Debug

```csharp
public static const BatchPreviewState Debug;
```

Preview the debug overlay render target.

**Returns** \
[BatchPreviewState](../../../Murder/Core/Graphics/BatchPreviewState.html) \

#### Gameplay

```csharp
public static const BatchPreviewState Gameplay;
```

Preview the gameplay sprite batch after the world is rendered but before UI compositing.

**Returns** \
[BatchPreviewState](../../../Murder/Core/Graphics/BatchPreviewState.html) \

#### Lights

```csharp
public static const BatchPreviewState Lights;
```

Preview the lighting render target.

**Returns** \
[BatchPreviewState](../../../Murder/Core/Graphics/BatchPreviewState.html) \

#### None

```csharp
public static const BatchPreviewState None;
```

No preview override; renders the final composited output normally.

**Returns** \
[BatchPreviewState](../../../Murder/Core/Graphics/BatchPreviewState.html) \

#### Reflected

```csharp
public static const BatchPreviewState Reflected;
```

Preview the reflected-world render target.

**Returns** \
[BatchPreviewState](../../../Murder/Core/Graphics/BatchPreviewState.html) \

#### Reflection

```csharp
public static const BatchPreviewState Reflection;
```

Preview the reflection mask/plane render target.

**Returns** \
[BatchPreviewState](../../../Murder/Core/Graphics/BatchPreviewState.html) \

#### Step1

```csharp
public static const BatchPreviewState Step1;
```

Preview the render target after the first pipeline step (main game buffer before post-processing).

**Returns** \
[BatchPreviewState](../../../Murder/Core/Graphics/BatchPreviewState.html) \

#### Step2

```csharp
public static const BatchPreviewState Step2;
```

Preview the render target after the second pipeline step (final target before UI).

**Returns** \
[BatchPreviewState](../../../Murder/Core/Graphics/BatchPreviewState.html) \

#### Step3

```csharp
public static const BatchPreviewState Step3;
```

Preview the render target after the third pipeline step.

**Returns** \
[BatchPreviewState](../../../Murder/Core/Graphics/BatchPreviewState.html) \

#### Ui

```csharp
public static const BatchPreviewState Ui;
```

Preview the UI render target in isolation.

**Returns** \
[BatchPreviewState](../../../Murder/Core/Graphics/BatchPreviewState.html) \

⚡
