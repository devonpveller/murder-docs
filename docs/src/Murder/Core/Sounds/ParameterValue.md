# ParameterValue

**Namespace:** Murder.Core.Sounds \
**Assembly:** Murder.dll

```csharp
public sealed struct ParameterValue
```

Pairs an audio parameter (`ParameterId`) with the value it should be set to. Declared inside `ISoundPlayer.cs` alongside `PlayEventInfo`, whose `Parameter` property carries this value.

**Intent:** Set an initial parameter value at the exact moment a sound event starts, instead of playing the event and then calling `SetParameter` separately on a following frame.

**Use-case:** `SoundServices.PlayWithParameter<T>` builds a `ParameterValue` from a `ParameterId` and a generic value (converted to `float`) and passes it through `PlayEventInfo.Parameter` to `ISoundPlayer.PlayEvent`, so e.g. a footstep event can be played with its "surface" parameter pre-set in the same call instead of racing a separate `SetParameter` call against the event actually starting.

### ⭐ Constructors

```csharp
public ParameterValue(ParameterId id, float value)
```

Creates a `ParameterValue` pairing a parameter with the value it should be set to.

**Parameters** \
`id` [ParameterId](../../../Murder/Core/Sounds/ParameterId.html) \
The parameter being targeted. \
`value` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
The value to assign to the parameter.

### ⭐ Properties

#### Id

```csharp
public readonly ParameterId Id;
```

The parameter being targeted.

**Returns** \
[ParameterId](../../../Murder/Core/Sounds/ParameterId.html) \

#### Value

```csharp
public readonly float Value;
```

The value to assign to `Id`.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

⚡
