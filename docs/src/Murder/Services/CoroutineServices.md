# CoroutineServices

**Namespace:** Murder.Services \
**Assembly:** Murder.dll

```csharp
public static class CoroutineServices
```

Extension methods for starting and scheduling coroutines — `IEnumerator<Wait>` sequences that resume across frames — on entities and on the `World`.

**Intent:** Provides the primary entry points into Murder's coroutine system, letting game code express "run this, possibly waiting between frames or seconds" logic without manually writing a state machine or system. `RunCoroutine` starts an arbitrary routine; `FireAfter`, `FireNextFrame`, `FireAfterFrames`, and `FireForDuration` are convenience wrappers around common waiting patterns (delay, next frame, N frames, or "run every frame for a duration with progress").

**Use-case:** Call `world.RunCoroutine(...)` for a coroutine that isn't tied to any single entity's lifetime (e.g. a scene transition or timed spawner). Call `entity.RunCoroutine(...)` to attach a coroutine driven by a `StateMachineComponent<CoroutineStateMachine>` on that entity, so it naturally stops if the entity is destroyed. Use `FireAfter`/`FireNextFrame`/`FireAfterFrames` instead of writing a full coroutine when you just need to defer a single `Action` by time or frames, and `FireForDuration` when you need a callback driven with the elapsed time each frame (e.g. animating a value over a fixed duration).

### ⭐ Methods

#### RunCoroutine(World, IEnumerator&lt;Wait&gt;, CoroutineFlags)

```csharp
public static Coroutine RunCoroutine(this World world, IEnumerator<Wait> routine, CoroutineFlags flags = CoroutineFlags.None)
```

Starts `routine` as a world-level coroutine via `MonoWorld.RunCoroutine`. Requires `world` to be a `MonoWorld` — logs a warning and returns a default (no-op) `Coroutine` otherwise. Pass `CoroutineFlags.DoNotPause` when the coroutine must keep advancing even while the game is paused (e.g. UI or menu-driven logic).

**Parameters** \
`world` [World](../../Bang/World.html) \
`routine` [IEnumerator\<Wait\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Generic.IEnumerator-1?view=net-7.0) \
`flags` [CoroutineFlags](../../Murder/Services/CoroutineFlags.html) \

**Returns** \
[Coroutine](../../Murder/Core/Coroutine.html) \

#### RunCoroutine(Entity, IEnumerator&lt;Wait&gt;)

```csharp
public static Entity RunCoroutine(this Entity e, IEnumerator<Wait> routine)
```

Attaches `routine` to `e` by setting a `StateMachineComponent<CoroutineStateMachine>` on it, then immediately ticks the state machine once so the coroutine starts executing this frame instead of waiting for the next system update. The coroutine's lifetime is tied to the entity: it stops advancing once the entity is destroyed or the component is removed. Returns `e` to allow chaining.

**Parameters** \
`e` [Entity](../../Bang/Entities/Entity.html) \
`routine` [IEnumerator\<Wait\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Generic.IEnumerator-1?view=net-7.0) \

**Returns** \
[Entity](../../Bang/Entities/Entity.html) \

#### FireAfter(World, float, Action, CoroutineFlags)

```csharp
public static Coroutine FireAfter(this World world, float seconds, Action action, CoroutineFlags flags = CoroutineFlags.None)
```

Invokes `action` once, after waiting `seconds` of game time. If `seconds` is `0`, `action` is invoked synchronously and no coroutine is started. Otherwise this schedules a coroutine that yields `Wait.ForSeconds(seconds)` before calling `action`. This is the go-to helper for "do this thing later" without hand-writing an `IEnumerator<Wait>`.

**Parameters** \
`world` [World](../../Bang/World.html) \
`seconds` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`action` [Action](https://learn.microsoft.com/en-us/dotnet/api/System.Action?view=net-7.0) \
`flags` [CoroutineFlags](../../Murder/Services/CoroutineFlags.html) \

**Returns** \
[Coroutine](../../Murder/Core/Coroutine.html) \

#### FireNextFrame(World, Action, CoroutineFlags)

```csharp
public static Coroutine FireNextFrame(this World world, Action action, CoroutineFlags flags = CoroutineFlags.None)
```

Shorthand for `FireAfterFrames(world, 1, action, flags)` — invokes `action` on the very next frame update. Useful for deferring logic that must not run mid-iteration (e.g. destroying or reparenting entities while a system is still iterating over the current frame's entities).

**Parameters** \
`world` [World](../../Bang/World.html) \
`action` [Action](https://learn.microsoft.com/en-us/dotnet/api/System.Action?view=net-7.0) \
`flags` [CoroutineFlags](../../Murder/Services/CoroutineFlags.html) \

**Returns** \
[Coroutine](../../Murder/Core/Coroutine.html) \

#### FireAfterFrames(World, int, Action, CoroutineFlags)

```csharp
public static Coroutine FireAfterFrames(this World world, int frames, Action action, CoroutineFlags flags = CoroutineFlags.None)
```

Invokes `action` once, after `frames` frame updates have elapsed. If `frames` is `0`, `action` runs synchronously immediately. Prefer this over `FireAfter` when the delay should be measured in frames rather than wall-clock/game time (e.g. waiting exactly one render frame for a texture to be ready).

**Parameters** \
`world` [World](../../Bang/World.html) \
`frames` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`action` [Action](https://learn.microsoft.com/en-us/dotnet/api/System.Action?view=net-7.0) \
`flags` [CoroutineFlags](../../Murder/Services/CoroutineFlags.html) \

**Returns** \
[Coroutine](../../Murder/Core/Coroutine.html) \

#### FireForDuration(World, float, Action&lt;float&gt;, CoroutineFlags)

```csharp
public static Coroutine FireForDuration(this World world, float duration, Action<float> action, CoroutineFlags flags = CoroutineFlags.None)
```

Runs `action` every frame for `duration` seconds, passing the elapsed time (clamped to `[0, duration]`) on each call, until the elapsed time reaches `duration`. Logs a warning and does nothing useful if `duration` is `0`. Use this for simple time-driven effects (fades, tweens, progress bars) where you don't want to write a full easing/animation component — the callback receives the elapsed time each frame so it can compute its own progress ratio.

**Parameters** \
`world` [World](../../Bang/World.html) \
`duration` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`action` [Action\<float\>](https://learn.microsoft.com/en-us/dotnet/api/System.Action-1?view=net-7.0) \
`flags` [CoroutineFlags](../../Murder/Services/CoroutineFlags.html) \

**Returns** \
[Coroutine](../../Murder/Core/Coroutine.html) \

⚡
