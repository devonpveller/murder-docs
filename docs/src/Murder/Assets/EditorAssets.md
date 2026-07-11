# EditorAssets

**Namespace:** Murder.Assets \
**Assembly:** Murder.dll

```csharp
public class EditorAssets
```

Holds references to all sprite and UI assets used exclusively by the Murder editor, such as cursor icons, dialogue node icons, and button sprites.

**Intent:** Centralise the GUIDs of every built-in editor sprite so they can be updated in one place without touching editor code that uses them.

**Use-case:** Access this class through `GameProfile.EditorAssets` to look up sprite GUIDs for custom editor widgets (e.g. `EditorAssets.Hand` for a hand cursor sprite), or override default assets by replacing the GUIDs in the editor.

### ⭐ Constructors
```csharp
public EditorAssets()
```

### ⭐ Properties
#### AnchorImage
```csharp
public readonly Guid AnchorImage;
```

Sprite GUID for the anchor point icon displayed in the cutscene editor.

**Returns** \
[Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \
#### BoxBg
```csharp
public readonly NineSliceInfo BoxBg;
```

Nine-slice sprite info for the default editor panel background box.

**Returns** \
[NineSliceInfo](../../Murder/Core/Graphics/NineSliceInfo.html) \
#### BoxBgGrayed
```csharp
public readonly NineSliceInfo BoxBgGrayed;
```

Nine-slice sprite info for the grayed/disabled editor panel background box.

**Returns** \
[NineSliceInfo](../../Murder/Core/Graphics/NineSliceInfo.html) \
#### BoxBgHovered
```csharp
public readonly NineSliceInfo BoxBgHovered;
```

Nine-slice sprite info for the hovered-state editor panel background box.

**Returns** \
[NineSliceInfo](../../Murder/Core/Graphics/NineSliceInfo.html) \
#### BoxBgSelected
```csharp
public readonly NineSliceInfo BoxBgSelected;
```

Nine-slice sprite info for the selected-state editor panel background box.

**Returns** \
[NineSliceInfo](../../Murder/Core/Graphics/NineSliceInfo.html) \
#### CutsceneImage
```csharp
public readonly Guid CutsceneImage;
```

Sprite GUID for the cutscene node icon displayed in the dialogue editor.

**Returns** \
[Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \
#### DialogueBtnPlay
```csharp
public readonly Guid DialogueBtnPlay;
```

Sprite GUID for the play button in the dialogue preview toolbar.

**Returns** \
[Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \
#### DialogueBtnStepBack
```csharp
public readonly Guid DialogueBtnStepBack;
```

Sprite GUID for the step-back button in the dialogue preview toolbar.

**Returns** \
[Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \
#### DialogueBtnStepForward
```csharp
public readonly Guid DialogueBtnStepForward;
```

Sprite GUID for the step-forward button in the dialogue preview toolbar.

**Returns** \
[Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \
#### DialogueIconAction
```csharp
public readonly Guid DialogueIconAction;
```

Sprite GUID for the action node icon in the dialogue graph editor.

**Returns** \
[Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \
#### DialogueIconBaloon
```csharp
public readonly Guid DialogueIconBaloon;
```

Sprite GUID for the speech balloon node icon in the dialogue graph editor.

**Returns** \
[Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \
#### DialogueIconEdgeChoice
```csharp
public readonly Guid DialogueIconEdgeChoice;
```

Sprite GUID for the choice-branch edge icon in the dialogue graph editor.

**Returns** \
[Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \
#### DialogueIconEdgeIf
```csharp
public readonly Guid DialogueIconEdgeIf;
```

Sprite GUID for the conditional (if) edge icon in the dialogue graph editor.

**Returns** \
[Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \
#### DialogueIconEdgeNext
```csharp
public readonly Guid DialogueIconEdgeNext;
```

Sprite GUID for the sequential (next) edge icon in the dialogue graph editor.

**Returns** \
[Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \
#### DialogueIconEdgeRandom
```csharp
public readonly Guid DialogueIconEdgeRandom;
```

Sprite GUID for the random-branch edge icon in the dialogue graph editor.

**Returns** \
[Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \
#### DialogueIconEdgeScore
```csharp
public readonly Guid DialogueIconEdgeScore;
```

Sprite GUID for the score-weighted edge icon in the dialogue graph editor.

**Returns** \
[Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \
#### DialogueIconExit
```csharp
public readonly Guid DialogueIconExit;
```

Sprite GUID for the exit node icon in the dialogue graph editor.

**Returns** \
[Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \
#### DialogueIconFlow
```csharp
public readonly Guid DialogueIconFlow;
```

Sprite GUID for the flow control node icon in the dialogue graph editor.

**Returns** \
[Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \
#### DialogueIconHello
```csharp
public readonly Guid DialogueIconHello;
```

Sprite GUID for the conversation-start node icon in the dialogue graph editor.

**Returns** \
[Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \
#### Eye
```csharp
public Guid Eye;
```

Sprite GUID for the eye/visibility cursor used in editor modes.

**Returns** \
[Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \
#### Hand
```csharp
public Guid Hand;
```

Sprite GUID for the hand/grab cursor used in editor pan/drag modes.

**Returns** \
[Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \
#### MusicImage
```csharp
public readonly Guid MusicImage;
```

Sprite GUID for the music/audio icon used in the dialogue editor's audio nodes.

**Returns** \
[Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \
#### Normal
```csharp
public Guid Normal;
```

Sprite GUID for the default (arrow) cursor used in standard editor modes.

**Returns** \
[Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \
#### Point
```csharp
public Guid Point;
```

Sprite GUID for the precision-point cursor used when placing entities or anchors.

**Returns** \
[Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \
#### SoundImage
```csharp
public readonly Guid SoundImage;
```

Sprite GUID for the sound/SFX icon used in the dialogue editor's audio nodes.

**Returns** \
[Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \


⚡