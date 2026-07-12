# SoundSpatialAttributes

**Namespace:** Murder.Core.Sounds \
**Assembly:** Murder.dll

```csharp
public sealed struct SoundSpatialAttributes
```

A snapshot of the position, facing, and velocity of a sound emitter or listener, in the units the audio middleware expects. Every play/update/listener call in `ISoundPlayer` that needs spatialization takes one of these instead of an `Entity` or `Vector2` directly, so the sound back-end has no dependency on Bang/ECS types.

**Intent:** Carry 3D spatial audio data (position, facing, velocity) for a sound emitter or listener, independent of any specific entity representation.

**Use-case:** Built via `SoundServices.GetSpatialAttributes(Entity?)`/`GetSpatialAttributes(Vector2)`/`GetSpatialAttributes(Vector3)`, which read an entity's `PositionComponent`/facing (or a raw position) and pack them into a `SoundSpatialAttributes`. `SoundServices.UpdateListenerPosition` passes one to `ISoundPlayer.UpdateListener` every frame with the camera/player position, and `SoundServices.TrackEventSourcePosition` passes one to `ISoundPlayer.UpdateEvent` so a playing sound instance keeps panning/attenuating correctly as its source entity moves. `Position` uses a `Vector3` (not `Vector2`) so callers can carry a Z/depth or "distance from camera" component even though gameplay itself is 2D — `SoundServices.ToListenerVector3` sets that third component to a fixed listener depth of `1`.

### ⭐ Properties

#### Direction

```csharp
public Direction Direction;
```

Forwards orientation, must be of unit length (1.0) and perpendicular to up.

**Returns** \
[Direction](../../../Murder/Helpers/Direction.html) \

#### Position

```csharp
public Vector3 Position;
```

Position in 2D space (with an extra Z component consumed by the audio middleware, e.g. for distance/depth). Used for panning and attenuation.

**Returns** \
[Vector3](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector3?view=net-7.0) \

#### Velocity

```csharp
public Vector2 Velocity;
```

Velocity in 2D space. Used for doppler effect.

**Returns** \
[Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

⚡
