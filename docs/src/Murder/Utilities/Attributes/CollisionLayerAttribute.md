# CollisionLayerAttribute

**Namespace:** Murder.Utilities.Attributes \
**Assembly:** Murder.dll

```csharp
public class CollisionLayerAttribute : Attribute
```

Use to signal an Int field to use a drop down selector using constant fields of any class deriving from [CollisionLayersBase](../../../Murder/Core/Physics/CollisionLayersBase.html)

**Intent:** Marks an integer field as a collision layer bitmask.

**Use-case:** Apply to an int field in a component to show a layer-picker dropdown in the editor, drawn from any class derived from `CollisionLayersBase`.

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