# OnBeforeReplaceMessage

**Namespace:** Murder.Messages \
**Assembly:** Murder.dll

```csharp
public sealed struct OnBeforeReplaceMessage : IMessage
```

A marker message with no payload sent to an entity immediately before its components are about to be wiped out and replaced by a fresh instantiation of a prefab.

**Intent:** Give systems that hold auxiliary, entity-keyed state (such as a collision cache) a chance to clean up or emit closing events before that state is invalidated by a component replace, since the replace itself does not go through the normal "entity destroyed" path.

**Use-case:** `PrefabAsset.Replace(world, e)` sends this (`e.SendOnBeforeReplaceMessage()`) right before calling `_entity.Create(world, e)` to re-instantiate the prefab's components onto the existing entity `e`. `TriggerPhysicsSystem` listens for it (`[Messager(typeof(OnBeforeReplaceMessage))]`) so that, before the entity's `CollisionCacheComponent` is discarded by the replace, `OnCollisionMessage` exit events are still sent for every entity it was colliding with — otherwise those exits would silently never fire. Pair with [OnReplacedMessage](../../Murder/Messages/OnReplacedMessage.html), which is sent right after the replace completes.

**Implements:** _[IMessage](../../Bang/Components/IMessage.html)_

⚡
