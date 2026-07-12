# WindowRefreshTrackerComponent

**Namespace:** Murder.Components \
**Assembly:** Murder.dll

```csharp
public sealed struct WindowRefreshTrackerComponent : IModifiableComponent, IComponent
```

Bridges the active scene's window-refresh event into Bang's reactive component notification system.

**Intent:** Let UI/layout systems subscribe to "the game window was resized/refreshed" through the normal component `Subscribe`/`Unsubscribe` pattern, instead of reaching into the active scene directly.

**Use-case:** Added once per world (it is marked `[Unique]`) to let UI layout systems re-calculate element positions and sizes whenever the window dimensions change; `Subscribe` forwards to `Scene.AddOnWindowRefresh`, which fires whenever `Scene.OnClientWindowChanged` runs. Note that `Unsubscribe` clears **all** window-refresh callbacks registered on the scene (`Scene.ResetWindowRefreshEvents`), not just the one passed in — the scene has no per-callback removal, only a full reset.

**Implements:** _[IModifiableComponent](../../Bang/Components/IModifiableComponent.html), [IComponent](../../Bang/Components/IComponent.html)_

### ⭐ Methods

#### Subscribe(Action)

```csharp
public virtual void Subscribe(Action notification)
```

Registers `notification` to be invoked whenever the active scene's window is resized or refreshed.

**Parameters** \
`notification` [Action](https://learn.microsoft.com/en-us/dotnet/api/System.Action?view=net-7.0) \

#### Unsubscribe(Action)

```csharp
public virtual void Unsubscribe(Action notification)
```

Clears all window-refresh callbacks registered on the active scene. The `notification` parameter is unused; it exists only to satisfy the `IModifiableComponent` subscription pattern.

**Parameters** \
`notification` [Action](https://learn.microsoft.com/en-us/dotnet/api/System.Action?view=net-7.0) \

⚡
