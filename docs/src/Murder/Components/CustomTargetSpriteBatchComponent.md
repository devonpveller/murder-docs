# CustomTargetSpriteBatchComponent

**Namespace:** Murder.Components \
**Assembly:** Murder.dll

```csharp
public sealed struct CustomTargetSpriteBatchComponent : IComponent
```

Overrides the sprite batch that an entity's sprite is rendered into.

**Implements:** _[IComponent](../../Bang/Components/IComponent.html)_

**Intent:** Redirects an entity's sprite to a specific `Batch2D` layer so it can be rendered at a different depth or with different post-processing than the default gameplay batch.

**Use-case:** Attach to a sprite entity that should render into a UI or foreground batch rather than the default gameplay batch; set `TargetBatch` to the desired `Batches2D` index.

### ⭐ Constructors

```csharp
public CustomTargetSpriteBatchComponent(int targetBatch)
```

**Parameters** \
`targetBatch` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

### ⭐ Properties

#### TargetBatch

```csharp
public readonly int TargetBatch;
```

Index of the `Batch2D` that this entity's sprite should be submitted to during rendering.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

⚡
