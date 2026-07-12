# Line

**Namespace:** Murder.Core.Dialogs \
**Assembly:** Murder.dll

```csharp
public sealed struct Line
```

A single authored line of dialogue, holding the speaker identity, optional portrait key, sound event, display text, optional timing delay, and an optional action to fire before the line plays.

**Intent:** Represents the smallest displayable unit in a dialogue script: who says what, which portrait and sound to use, how long to pause, and any side effect (like a `DialogAction`) that should run right before it is shown.

**Use-case:** Stored in `Dialog.Lines`; the dialogue system iterates them in order via `CharacterRuntime.NextLine`, running `ActBeforeWith` (if set) and firing `Event`, then passes the line to the game's UI layer for display.

### ⭐ Constructors

```csharp
public Line()
```

Creates an empty line with no speaker, text, or delay.

```csharp
public Line(Guid? speaker)
```

Creates a line with only a speaker set; text, portrait, delay, and event are left unset.

**Parameters** \
`speaker` [Guid?](https://learn.microsoft.com/en-us/dotnet/api/System.Nullable-1?view=net-7.0) \

```csharp
public Line(LocalizedString text)
```

Create a line with a text without any speaker.

**Parameters** \
`text` [LocalizedString](../../../Murder/Assets/LocalizedString.html) \

```csharp
public Line(Guid speaker, LocalizedString text)
```

Create a line with a text. That won't be used as a timer.

**Parameters** \
`speaker` [Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \
`text` [LocalizedString](../../../Murder/Assets/LocalizedString.html) \

```csharp
public Line(Guid? speaker, float delay)
```

Create a line with a delay. That won't be used as a text. Used to insert a pause of `delay` seconds into the dialogue without displaying any text.

**Parameters** \
`speaker` [Guid?](https://learn.microsoft.com/en-us/dotnet/api/System.Nullable-1?view=net-7.0) \
`delay` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

```csharp
public Line(Guid? speaker, string? portrait, LocalizedString? text, float? delay, string? @event)
```

Full constructor that sets every field except `ActBeforeWith`; any field may be `null` to use the speaker's defaults.

**Parameters** \
`speaker` [Guid?](https://learn.microsoft.com/en-us/dotnet/api/System.Nullable-1?view=net-7.0) \
`portrait` [string?](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
`text` [LocalizedString?](../../../Murder/Assets/LocalizedString.html) \
`delay` [float?](https://learn.microsoft.com/en-us/dotnet/api/System.Nullable-1?view=net-7.0) \
`event` [string?](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

### ⭐ Properties

#### ActBeforeWith

```csharp
public readonly DialogAction? ActBeforeWith { get; init; }
```

Optional `DialogAction` (e.g. a blackboard mutation) that the runtime executes immediately before this line is shown; used for effects that should happen exactly when the line starts, such as setting a fact right before the text appears.

**Returns** \
[DialogAction?](../../../Murder/Core/Dialogs/DialogAction.html) \

#### Delay

```csharp
public readonly float? Delay;
```

Delay in seconds.

**Returns** \
[float?](https://learn.microsoft.com/en-us/dotnet/api/System.Nullable-1?view=net-7.0) \

#### Event

```csharp
public readonly string? Event;
```

Optional sound event that will be fired with this line, letting a line trigger a voice bark or SFX cue alongside its text.

**Returns** \
[string?](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### IsText

```csharp
public bool IsText { get; }
```

Returns `true` when `Text` is non-null, indicating this line carries displayable content rather than being a pure delay/timer line.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### Portrait

```csharp
public readonly string? Portrait;
```

Optional portrait key overriding the speaker's default; `null` means use the speaker's default portrait.

**Returns** \
[string?](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### Speaker

```csharp
public readonly Guid? Speaker;
```

GUID of the `SpeakerAsset` delivering this line; `null` if no speaker is associated.

**Returns** \
[Guid?](https://learn.microsoft.com/en-us/dotnet/api/System.Nullable-1?view=net-7.0) \

#### Text

```csharp
public readonly LocalizedString? Text;
```

If the caption has a text, this will be the information.

**Returns** \
[LocalizedString?](../../../Murder/Assets/LocalizedString.html) \

### ⭐ Methods

#### WithDelay(float)

```csharp
public Line WithDelay(float delay)
```

Returns a copy of this line with the `Delay` replaced (all other fields, including `ActBeforeWith`, are preserved).

**Parameters** \
`delay` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

**Returns** \
[Line](../../../Murder/Core/Dialogs/Line.html) \

#### WithEvent(string?)

```csharp
public Line WithEvent(string? @event)
```

Returns a copy of this line with the `Event` replaced.

**Parameters** \
`event` [string?](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

**Returns** \
[Line](../../../Murder/Core/Dialogs/Line.html) \

#### WithPortrait(string?)

```csharp
public Line WithPortrait(string? portrait)
```

Returns a copy of this line with the `Portrait` replaced.

**Parameters** \
`portrait` [string?](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

**Returns** \
[Line](../../../Murder/Core/Dialogs/Line.html) \

#### WithSpeaker(Guid)

```csharp
public Line WithSpeaker(Guid speaker)
```

Returns a copy of this line with the `Speaker` replaced.

**Parameters** \
`speaker` [Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \

**Returns** \
[Line](../../../Murder/Core/Dialogs/Line.html) \

#### WithSpeakerAndPortrait(Guid, string?)

```csharp
public Line WithSpeakerAndPortrait(Guid speaker, string? portrait)
```

Returns a copy of this line with both `Speaker` and `Portrait` replaced.

**Parameters** \
`speaker` [Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \
`portrait` [string?](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

**Returns** \
[Line](../../../Murder/Core/Dialogs/Line.html) \

#### WithText(LocalizedString)

```csharp
public Line WithText(LocalizedString text)
```

Returns a copy of this line with the `Text` replaced.

**Parameters** \
`text` [LocalizedString](../../../Murder/Assets/LocalizedString.html) \

**Returns** \
[Line](../../../Murder/Core/Dialogs/Line.html) \

⚡
