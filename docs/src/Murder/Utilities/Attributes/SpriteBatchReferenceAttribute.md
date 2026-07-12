# SpriteBatchReferenceAttribute

**Namespace:** Murder.Utilities.Attributes \
**Assembly:** Murder.dll

```csharp
public class SpriteBatchReferenceAttribute : Attribute
```

Marks an `int` field as a reference to a sprite batch layer from [Batch2D](../../../Murder/Core/Graphics/Batch2D.html).

**Intent:** Lets a component field pick a render/sprite-batch layer by name in the editor instead of remembering its integer id.

**Use-case:** Apply to an `int` field, such as `AgentSpriteComponent`'s or `DrawRectangleComponent`'s target batch field, so the editor's `IntField` shows a batch-layer picker populated from `AssetsFilter.SpriteBatches` instead of a raw numeric input, letting designers select which draw layer/batch an element renders into by name.

**Implements:** _[Attribute](https://learn.microsoft.com/en-us/dotnet/api/System.Attribute?view=net-7.0)_

### ⭐ Constructors

```csharp
public SpriteBatchReferenceAttribute()
```

### ⭐ Properties

#### TypeId

```csharp
public virtual Object TypeId { get; }
```

Unique object identity for this attribute type, inherited from `Attribute`.

**Returns** \
[Object](https://learn.microsoft.com/en-us/dotnet/api/System.Object?view=net-7.0) \

⚡
