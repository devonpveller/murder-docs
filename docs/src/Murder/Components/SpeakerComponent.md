# SpeakerComponent

**Namespace:** Murder.Components \
**Assembly:** Murder.dll

```csharp
public sealed struct SpeakerComponent : IComponent
```

Component for an entity that is able to speak with other elements.

**Intent:** Identify an entity as a dialogue speaker and link it to a [SpeakerAsset](../../Murder/Assets/SpeakerAsset.html) that defines its name and portrait.

**Use-case:** Attach to every character entity that can appear as a dialogue speaker (the interactor talking, or the entity being talked to). `TalkToInteraction` and `CharacterRuntime` both call `entity.TryGetSpeaker()` to resolve `SpeakerComponent.Speaker` into a `SpeakerAsset`, which supplies the display name and portrait shown in the dialogue UI while that entity is speaking.

**Implements:** _[IComponent](../../Bang/Components/IComponent.html)_

### ⭐ Constructors

```csharp
public SpeakerComponent(Guid speaker)
```

**Parameters** \
`speaker` [Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \

### ⭐ Properties

#### Speaker

```csharp
public readonly Guid Speaker;
```

GUID of the [SpeakerAsset](../../Murder/Assets/SpeakerAsset.html) that defines this entity's dialogue name and portrait.

**Returns** \
[Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \

⚡
