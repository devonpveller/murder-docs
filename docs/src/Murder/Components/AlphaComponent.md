# AlphaComponent

**Namespace:** Murder.Components \
**Assembly:** Murder.dll

```csharp
public sealed struct AlphaComponent : IComponent
```

Set alpha of a component being displayed in the screen.

**Implements:** _[IComponent](../../Bang/Components/IComponent.html)_

**Intent:** Stores a composite alpha value computed from multiple independent sources so any system can adjust transparency without overwriting another system's contribution.

**Use-case:** Attach to a sprite entity and use `Set(AlphaSources, float)` to let the fade system and the game logic each independently control opacity; the final `Alpha` is the product of all source values.

### ⭐ Constructors
```csharp
public AlphaComponent()
```

```csharp
public AlphaComponent(AlphaSources source, float amount)
```

Creates a component with `amount` applied to the specified `source` slot.

**Parameters** \
`source` [AlphaSources](../../Murder/Components/AlphaSources.html) \
`amount` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

```csharp
public AlphaComponent(Single[] sources)
```

Creates a component from a raw array of per-source alpha values.

**Parameters** \
`sources` [float[]](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

### ⭐ Properties
#### Alpha
```csharp
public float Alpha { get; }
```

The final composite alpha value, computed as the product of all source slots.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
### ⭐ Methods
#### Set(AlphaSources, float)
```csharp
public AlphaComponent Set(AlphaSources source, float amount)
```

Returns a new `AlphaComponent` with the value for `source` updated to `amount`.

**Parameters** \
`source` [AlphaSources](../../Murder/Components/AlphaSources.html) \
`amount` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

**Returns** \
[AlphaComponent](../../Murder/Components/AlphaComponent.html) \

#### Get(AlphaSources)
```csharp
public float Get(AlphaSources source)
```

Returns the alpha value currently stored for the given `source` slot.

**Parameters** \
`source` [AlphaSources](../../Murder/Components/AlphaSources.html) \

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \



⚡