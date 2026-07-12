# SoundParameterComponent

**Namespace:** Murder.Components \
**Assembly:** Murder.dll

```csharp
public sealed struct SoundParameterComponent : IComponent
```

Empty marker component with no fields.

**Intent:** A required-companion marker for `SetSoundParameterOnInteraction`, which declares `[Requires(typeof(SoundParameterComponent))]`. Bang's `[Requires]` attribute auto-adds the required component whenever the interaction is attached to an entity, so this component's only job is to make sure any entity carrying a `SetSoundParameterOnInteraction` also satisfies that requirement.

**Use-case:** You do not normally add this directly; it is added automatically whenever an entity gets a `SetSoundParameterOnInteraction` (e.g. an interactable prop configured in the editor to set a blackboard-driven sound rule action or a middleware parameter on interact). Also carries the `[Sound]` attribute (shared with `SoundComponent`, `AmbienceComponent`, `SoundShapeComponent`, etc.), which the editor uses via `EditorSoundServices`/`WorldAssetEditor_Sounds` to find and list all sound-related entities and components in its dedicated Sound editor tooling.

**Implements:** _[IComponent](../../Bang/Components/IComponent.html)_

⚡
