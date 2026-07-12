# SoundPlayerAttribute

**Namespace:** Murder.Utilities.Attributes \
**Assembly:** Murder.dll

```csharp
public class SoundPlayerAttribute : Attribute
```

Marks a component as a "sound playback hook": one whose presence causes sounds to be triggered by something other than the component itself, such as an animation frame marker or a dialogue line.

**Intent:** Lets the editor surface, group, and audition entities whose sounds are driven indirectly (through animation events or dialogue), so sound designers can find and preview them without knowing which gameplay system owns them.

**Use-case:** Apply to a component such as `EventListenerEditorComponent` (animation-event-driven sounds) or `SpeakerEditorListenerComponent` (dialogue-driven sounds). `AssetEditor` shows a speaker icon next to components carrying this attribute, `WorldAssetEditor_Sounds` groups the entities that carry them under "Entities with sound hooks" in the world editor's Sounds tab, and `SoundEditorSystem` uses it to find and drive playback preview for those entities in the editor.

**Implements:** _[Attribute](https://learn.microsoft.com/en-us/dotnet/api/System.Attribute?view=net-7.0)_

### ⭐ Constructors

```csharp
public SoundPlayerAttribute()
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
