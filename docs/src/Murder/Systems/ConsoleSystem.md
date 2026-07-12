# ConsoleSystem

**Namespace:** Murder.Systems \
**Assembly:** Murder.dll

```csharp
public class ConsoleSystem : IStartupSystem, ISystem, IGuiSystem, IRenderSystem
```

Initializes the in-game `GameLogger` console on startup and renders it as an overlay GUI each frame, allowing developers to enter and execute commands at runtime.

**Intent:** Provides an in-game debug console that developers can use to inspect and control the game state through typed commands.

**Use-case:** Include in development or debug worlds to enable the command console overlay; typically excluded from release builds.

**Implements:** _[IStartupSystem](../../Bang/Systems/IStartupSystem.html), [ISystem](../../Bang/Systems/ISystem.html), [IGuiSystem](../../Murder/Core/Graphics/IGuiSystem.html), [IRenderSystem](../../Bang/Systems/IRenderSystem.html)_

### ⭐ Constructors

```csharp
public ConsoleSystem()
```

### ⭐ Methods

#### DrawGui(RenderContext, Context)

```csharp
public virtual void DrawGui(RenderContext render, Context context)
```

Renders the developer console overlay and routes any submitted command string to `CommandServices.Parse`.

**Parameters** \
`render` [RenderContext](../../Murder/Core/Graphics/RenderContext.html) \
`context` [Context](../../Bang/Contexts/Context.html) \

#### Start(Context)

```csharp
public virtual void Start(Context context)
```

Obtains or creates the singleton `GameLogger` instance used by the console overlay.

**Parameters** \
`context` [Context](../../Bang/Contexts/Context.html) \

⚡
