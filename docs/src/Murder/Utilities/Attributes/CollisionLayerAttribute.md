# CollisionLayerAttribute

**Namespace:** Murder.Utilities.Attributes \
**Assembly:** Murder.dll

```csharp
public class CollisionLayerAttribute : Attribute
```

Marks an [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) field as a collision layer bitmask.

**Intent:** Lets a component field store a combination of collision layers with a friendly editor UI instead of a raw bitmask number.

**Use-case:** Apply to an `int` field that stores a mask of collision layers, such as `ColliderComponent`'s layer/mask fields or a raycast/overlap filter mask. The editor's `IntField` detects the attribute and draws one checkbox per layer constant declared on any class deriving from [CollisionLayersBase](../../../Murder/Core/Physics/CollisionLayersBase.html) (collected via `AssetsFilter.CollisionLayers`), OR-ing the checked constants together into the field's value, instead of requiring the designer to compute the bitmask by hand.

**Implements:** _[Attribute](https://learn.microsoft.com/en-us/dotnet/api/System.Attribute?view=net-7.0)_

### ⭐ Constructors

```csharp
public CollisionLayerAttribute()
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
