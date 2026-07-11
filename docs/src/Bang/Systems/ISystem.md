# ISystem

**Namespace:** Bang.Systems \
**Assembly:** Bang.dll

```csharp
public abstract ISystem
```

The root marker interface for all systems in the ECS. A system will run through all entities
            that satisfy its filters at once, rather than operating on entities one by one.
            [ISystem](../../Bang/Systems/ISystem.html) carries no members of its own: a class opts into concrete behavior
            by implementing one or more of the specialized interfaces declared alongside it -
            [IStartupSystem](../../Bang/Systems/IStartupSystem.html), [IUpdateSystem](../../Bang/Systems/IUpdateSystem.html), [IFixedUpdateSystem](../../Bang/Systems/IFixedUpdateSystem.html),
            [IRenderSystem](../../Bang/Systems/IRenderSystem.html), [IReactiveSystem](../../Bang/Systems/IReactiveSystem.html), [IMessagerSystem](../../Bang/Systems/IMessagerSystem.html),
            [IActivateAndDeactivateListenerSystem](../../Bang/Systems/IActivateAndDeactivateListenerSystem.html) and [IExitSystem](../../Bang/Systems/IExitSystem.html) - and by
            decorating the class with attributes such as [FilterAttribute](../../Bang/Systems/FilterAttribute.html),
            [WatchAttribute](../../Bang/Systems/WatchAttribute.html) and [MessagerAttribute](../../Bang/Systems/MessagerAttribute.html). [World](../../Bang/World.html) discovers
            which of these a system implements purely through reflection (see World_Reflection.cs) when the
            world is constructed, and uses that information to build the system's [Context](../../Bang/Contexts/Context.html)
            and to decide when and how to call it. This is why a game or an autonomous agent authoring a new
            system never derives from a base class: it simply implements the marker interfaces that describe
            what the system needs to do.



⚡
