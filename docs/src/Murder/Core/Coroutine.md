# Coroutine

**Namespace:** Murder.Core \
**Assembly:** Murder.dll \

```csharp
public readonly struct Coroutine
```

A lightweight handle to a coroutine started with `MonoWorld.RunCoroutine` (or one of the [CoroutineServices](../../Murder/Services/CoroutineServices.html) extension methods), returned so the caller can cancel it early with `Stop`. It does not hold the coroutine's state directly — it only tracks the pooled effect entity slot the coroutine is running on within the owning [MonoWorld](../../Murder/Core/MonoWorld.html).

**Intent:** Coroutines in Murder aren't backed by a language-level coroutine/async mechanism — each one is really a [CoroutineStateMachine](../../Murder/StateMachines/CoroutineStateMachine.html) attached to a pooled, invisible "effect entity" that `MonoWorld` manages internally. `Coroutine` is the opaque token callers get back instead of having to track that entity themselves; its only job is remembering which pooled slot to free when the coroutine is stopped.

**Use-case:** Hold on to the `Coroutine` returned by `world.RunCoroutine(...)`, `world.FireAfter(...)`, or a similar [CoroutineServices](../../Murder/Services/CoroutineServices.html) helper if you might need to cancel it before it finishes naturally (e.g. a timed effect that should stop early if the player leaves the area), then call `coroutine.Stop(world)`. If you never need to cancel it, you can discard the return value — the coroutine will keep running and clean itself up when its underlying routine completes. A default `Coroutine` (e.g. `default(Coroutine)`, or the value returned when `RunCoroutine` is called on a `World` that isn't a `MonoWorld`) has `Index == -1` and `Stop` on it is a safe no-op.

### ⭐ Constructors

#### Coroutine()

```csharp
public Coroutine()
```

Creates a default, no-op handle ([Index](../../Murder/Core/Coroutine.html#index) of `-1`) that [Stop(World)](../../Murder/Core/Coroutine.html#stopworld) silently ignores.

#### Coroutine(int)

```csharp
public Coroutine(int index)
```

Creates a handle pointing at the coroutine running on pooled effect entity slot `index`. Only `MonoWorld.RunCoroutine` should call this — game code should treat `Coroutine` as an opaque handle obtained from that call.

**Parameters** \
`index` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

### ⭐ Properties

#### Index

```csharp
public readonly int Index;
```

The pooled effect entity slot this coroutine is running on, or `-1` for a default/no-op handle (e.g. the one returned when a `RunCoroutine`/`Fire*` extension in [CoroutineServices](../../Murder/Services/CoroutineServices.html) is called on a [World](../../Bang/World.html) that isn't a [MonoWorld](../../Murder/Core/MonoWorld.html)).

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

### ⭐ Methods

#### Stop(World)

```csharp
public void Stop(World world)
```

Cancels this coroutine early, before it would otherwise finish on its own. Does nothing if this is a default/no-op handle ([Index](../../Murder/Core/Coroutine.html#index) of `-1`) or if `world` isn't a [MonoWorld](../../Murder/Core/MonoWorld.html).

**Parameters** \
`world` [World](../../Bang/World.html) \


⚡
