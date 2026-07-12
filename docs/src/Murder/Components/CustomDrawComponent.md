# CustomDrawComponent

**Namespace:** Murder.Components \
**Assembly:** Murder.dll

```csharp
public sealed struct CustomDrawComponent : IComponent
```

Holds a delegate that is invoked each render frame to perform arbitrary custom drawing for this entity.

**Implements:** _[IComponent](../../Bang/Components/IComponent.html)_

**Intent:** Lets code-driven entities supply their own render logic without needing a dedicated system or sprite asset.

**Use-case:** Attach at runtime and pass a lambda that calls `RenderContext` drawing methods; the render system will invoke it each frame for the owning entity.

### ⭐ Constructors

```csharp
public CustomDrawComponent(Action<T> draw)
```

**Parameters** \
`draw` [Action\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Action-1?view=net-7.0) \

### ⭐ Properties

#### Draw

```csharp
public readonly Action<T> Draw;
```

Delegate invoked with the current `RenderContext` to perform this entity's custom rendering.

**Returns** \
[Action\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Action-1?view=net-7.0) \

⚡
