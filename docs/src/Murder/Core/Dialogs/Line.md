# Line

**Namespace:** Murder.Core.Dialogs \
**Assembly:** Murder.dll

```csharp
public sealed struct Line
```

A single authored line of dialogue, holding the speaker identity, optional portrait key, display text, optional timing delay, and an optional pre-line action.

**Intent:** Represents the smallest displayable unit in a dialogue script: who says what, which portrait to show, and how long to pause before or after it.

**Use-case:** Stored in `Dialog.Lines`; the dialogue system iterates them in order via `CharacterRuntime.NextLine` and passes each to the game's UI layer for display.

### ⭐ Constructors
```csharp
public Line()
```

Creates an empty line with no speaker, text, or delay.

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
public Line(T? speaker, float delay)
```

Creates a timer-only line that pauses dialogue for `delay` seconds with no text.

**Parameters** \
`speaker` [T?](https://learn.microsoft.com/en-us/dotnet/api/System.Nullable-1?view=net-7.0) \
`delay` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

```csharp
public Line(T? speaker, string portrait, T? text, T? delay)
```

Full constructor that sets every field; any field may be `null` to use the speaker's defaults.

**Parameters** \
`speaker` [T?](https://learn.microsoft.com/en-us/dotnet/api/System.Nullable-1?view=net-7.0) \
`portrait` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
`text` [T?](https://learn.microsoft.com/en-us/dotnet/api/System.Nullable-1?view=net-7.0) \
`delay` [T?](https://learn.microsoft.com/en-us/dotnet/api/System.Nullable-1?view=net-7.0) \

```csharp
public Line(T? speaker)
```

Creates a line with only a speaker set; text and delay are left unset.

**Parameters** \
`speaker` [T?](https://learn.microsoft.com/en-us/dotnet/api/System.Nullable-1?view=net-7.0) \

### ⭐ Properties
#### Delay
```csharp
public readonly T? Delay;
```

Delay in seconds.

**Returns** \
[T?](https://learn.microsoft.com/en-us/dotnet/api/System.Nullable-1?view=net-7.0) \
#### IsText
```csharp
public bool IsText { get; }
```

Returns `true` when `Text` is non-null, indicating this line carries displayable content.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
#### Portrait
```csharp
public readonly string Portrait;
```

Optional portrait key overriding the speaker's default; `null` means use the speaker's default portrait.

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
#### Speaker
```csharp
public readonly T? Speaker;
```

GUID of the `SpeakerAsset` delivering this line; `null` if no speaker is associated.

**Returns** \
[T?](https://learn.microsoft.com/en-us/dotnet/api/System.Nullable-1?view=net-7.0) \
#### Text
```csharp
public readonly T? Text;
```

If the caption has a text, this will be the information.

**Returns** \
[T?](https://learn.microsoft.com/en-us/dotnet/api/System.Nullable-1?view=net-7.0) \
### ⭐ Methods
#### WithDelay(float)
```csharp
public Line WithDelay(float delay)
```

Returns a copy of this line with the `Delay` replaced.

**Parameters** \
`delay` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

**Returns** \
[Line](../../../Murder/Core/Dialogs/Line.html) \

#### WithPortrait(string)
```csharp
public Line WithPortrait(string portrait)
```

Returns a copy of this line with the `Portrait` replaced.

**Parameters** \
`portrait` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

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

#### WithSpeakerAndPortrait(Guid, string)
```csharp
public Line WithSpeakerAndPortrait(Guid speaker, string portrait)
```

Returns a copy of this line with both `Speaker` and `Portrait` replaced.

**Parameters** \
`speaker` [Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \
`portrait` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

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