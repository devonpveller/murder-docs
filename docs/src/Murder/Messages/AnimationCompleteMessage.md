# AnimationCompleteMessage

**Namespace:** Murder.Messages \
**Assembly:** Murder.dll

```csharp
public sealed struct AnimationCompleteMessage : IMessage
```

Sent by sprite systems when an animation finishes playing, carrying information about how it completed.

**Intent:** Notify listening systems that an entity's current animation has reached its last frame.

**Use-case:** Listen for this message in gameplay systems to trigger follow-up logic—such as destroying a projectile after its impact animation completes, or chaining a walk animation into an idle animation once a movement sequence finishes.

**Implements:** _[IMessage](../../Bang/Components/IMessage.html)_



⚡