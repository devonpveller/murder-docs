# CoroutineServices

**Namespace:** Murder.Services \
**Assembly:** Murder.dll

```csharp
public static class CoroutineServices
```

Provides extension methods for starting coroutines on entities and worlds.

**Intent:** Simplifies scheduling time-deferred or frame-deferred logic in the ECS world.

**Use-case:** Call `RunCoroutine` on an entity to run a state-machine coroutine tied to that entity's lifetime, or on a world to run a global coroutine for timed events like scene transitions.

### ⭐ Methods
#### RunCoroutine(Entity, IEnumerator<T>)
```csharp
public void RunCoroutine(Entity e, IEnumerator<T> routine)
```
Attaches a coroutine state machine to the entity so it executes every frame until complete.

**Parameters** \
`e` [Entity](../../Bang/Entities/Entity.html) \
`routine` [IEnumerator\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Generic.IEnumerator-1?view=net-7.0) \

#### RunCoroutine(World, IEnumerator<T>)
```csharp
public void RunCoroutine(World world, IEnumerator<T> routine)
```
Runs a coroutine at the world level (without binding it to a specific entity).

**Parameters** \
`world` [World](../../Bang/World.html) \
`routine` [IEnumerator\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Generic.IEnumerator-1?view=net-7.0) \



⚡