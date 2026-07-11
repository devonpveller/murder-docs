# AnimationSpeedOverload

**Namespace:** Murder.Components \
**Assembly:** Murder.dll

```csharp
public sealed struct AnimationSpeedOverload : IComponent
```

Makes that the animation plays at a different rate.

**Implements:** _[IComponent](../../Bang/Components/IComponent.html)_

**Intent:** Overrides the playback speed of an entity's sprite animation, making it play faster or slower than its authored rate.

**Use-case:** Attach to slow down an animation during a slow-motion effect or speed it up to match a gameplay state; set `Persist` to `true` if the override should survive scene transitions.

### ⭐ Constructors
```csharp
public AnimationSpeedOverload(float rate, bool persist)
```

**Parameters** \
`rate` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`persist` [bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

### ⭐ Properties
#### Persist
```csharp
public readonly bool Persist;
```

When `true`, this speed overload is kept across scene transitions; when `false` it is discarded on reload.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
#### Rate
```csharp
public readonly float Rate;
```

Playback speed multiplier; `1.0` is normal speed, `2.0` is double speed, `0.5` is half speed.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \


⚡