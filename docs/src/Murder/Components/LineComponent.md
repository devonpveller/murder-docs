# LineComponent

**Namespace:** Murder.Components \
**Assembly:** Murder.dll

```csharp
public sealed struct LineComponent : IComponent
```

Holds the dialogue `Line` data that the entity is currently delivering, along with the time at which delivery started.

**Intent:** Carry a single dialogue line to be displayed by the dialogue render system, with a timestamp for timed text effects.

**Use-case:** Added to the dialogue entity by the dialogue system when a new line begins; read `Line` to get the text/speaker data and `Start` to compute how much of the line has elapsed.

**Implements:** _[IComponent](../../Bang/Components/IComponent.html)_

### ⭐ Constructors
```csharp
public LineComponent(Line line, float start)
```

**Parameters** \
`line` [Line](../../Murder/Core/Dialogs/Line.html) \
`start` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

### ⭐ Properties
#### Line
```csharp
public readonly Line Line;
```

The dialogue line data, including speaker and text content.

**Returns** \
[Line](../../Murder/Core/Dialogs/Line.html) \
#### Start
```csharp
public readonly float Start;
```

Absolute game time (in seconds) when this line began playing, used to drive typewriter or timed display effects.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \


⚡