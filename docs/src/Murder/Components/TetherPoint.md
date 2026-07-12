# TetherPoint

**Namespace:** Murder.Components \
**Assembly:** Murder.dll

```csharp
public sealed struct TetherPoint
```

Represents a single tether point for an entity.

**Intent:** Describe one tether constraint: which entity to pull towards, and the desired separation distance between the two.

**Use-case:** Construct one per tether target and add to the `TetherPoints` array of a [TetheredComponent](../../Murder/Components/TetheredComponent.html); the entity carrying that component is nudged towards `Target` whenever they drift further apart than `Length` allows.

### ⭐ Constructors

```csharp
public TetherPoint(int target, float distance, float maxAngleDeviation, float snapDistance)
```

Creates a tether constraint pointing at `target` with the given separation distance. `maxAngleDeviation` and `snapDistance` are stored but not currently read by the tether resolution system — they are reserved for future angle- and snap-based tether behavior.

**Parameters** \
`target` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`distance` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`maxAngleDeviation` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`snapDistance` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

### ⭐ Properties

#### Length

```csharp
public readonly float Length;
```

The desired separation distance from `Target`. The tether-resolution system pulls this entity and its target towards each other whenever they are further apart than `Length`.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### MaxAngleDeviation

```csharp
public readonly float MaxAngleDeviation;
```

Reserved for a future angle-constrained tether, intended to cap how far the tether can deviate from the target's facing direction. Stored on the struct but not currently read by the tether-resolution system.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### SnapDistance

```csharp
public readonly float SnapDistance;
```

Reserved for a future snap-to-target behavior. Stored on the struct but not currently read by the tether-resolution system.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### Target

```csharp
public readonly int Target;
```

The entity ID this tether pulls the owning entity towards. If the target entity cannot be found in the world when the tether-resolution system runs, this tether point is skipped for that tick and a warning is logged.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

⚡
