# OnReplacedMessage

**Namespace:** Murder.Messages \
**Assembly:** Murder.dll

```csharp
public sealed struct OnReplacedMessage : IMessage
```

A marker message with no payload sent to an entity right after its components have been replaced by a fresh instantiation of a prefab.

**Intent:** Let systems react once an entity's components have finished being swapped out for a new prefab's components, since a replace is not a destroy/create cycle and would otherwise be invisible to reactive systems watching for entity creation.

**Use-case:** `PrefabAsset.Replace(world, e)` sends this (`e.SendOnReplacedMessage()`) immediately after `_entity.Create(world, e)` finishes re-instantiating the prefab's components onto entity `e`. Listen for it with `[Messager(typeof(OnReplacedMessage))]` to run initialization logic that must happen after a replace, mirroring what an `OnAdded`/startup system would normally do for a freshly created entity. Paired with [OnBeforeReplaceMessage](../../Murder/Messages/OnBeforeReplaceMessage.html), which is sent just before the replace happens.

**Implements:** _[IMessage](../../Bang/Components/IMessage.html)_

⚡
