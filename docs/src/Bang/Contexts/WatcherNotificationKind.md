# WatcherNotificationKind

**Namespace:** Bang.Contexts \
**Assembly:** Bang.dll

```csharp
public sealed enum WatcherNotificationKind : Enum, IComparable, ISpanFormattable, IFormattable, IConvertible
```

When a system is watching for a component, this is the kind of notification currently fired. The order
of the enumerator dictates the order that these will be called on the watcher systems. Notifications are
produced internally by a component watcher as it observes a [Context](../../Bang/Contexts/Context.html),
and consumed once per frame, batched by entity, by
[IReactiveSystem](../../Bang/Systems/IReactiveSystem.html) (via its
OnAdded/OnRemoved/OnModified/OnActivated/OnDeactivated callbacks) during the world's notification pass.
A system opts into these notifications for a given component by declaring
[WatchAttribute](../../Bang/Systems/WatchAttribute.html).

**Implements:** _[Enum](https://learn.microsoft.com/en-us/dotnet/api/System.Enum?view=net-7.0), [IComparable](https://learn.microsoft.com/en-us/dotnet/api/System.IComparable?view=net-7.0), [ISpanFormattable](https://learn.microsoft.com/en-us/dotnet/api/System.ISpanFormattable?view=net-7.0), [IFormattable](https://learn.microsoft.com/en-us/dotnet/api/System.IFormattable?view=net-7.0), [IConvertible](https://learn.microsoft.com/en-us/dotnet/api/System.IConvertible?view=net-7.0)_

### ⭐ Properties
#### Added
```csharp
public static const WatcherNotificationKind Added;
```

Component has been added. It is not called if the entity is dead. Maps to
[IReactiveSystem](../../Bang/Systems/IReactiveSystem.html)'s `OnAdded` callback.

**Returns** \
[WatcherNotificationKind](../../Bang/Contexts/WatcherNotificationKind.html) \
#### Disabled
```csharp
public static const WatcherNotificationKind Disabled;
```

Entity has been disabled, hence all its components. Maps to
[IReactiveSystem](../../Bang/Systems/IReactiveSystem.html)'s `OnDeactivated` callback.

**Returns** \
[WatcherNotificationKind](../../Bang/Contexts/WatcherNotificationKind.html) \
#### Enabled
```csharp
public static const WatcherNotificationKind Enabled;
```

Entity has been enabled, hence all its components. Called if an entity was
            previously disabled. Maps to [IReactiveSystem](../../Bang/Systems/IReactiveSystem.html)'s
`OnActivated` callback.

**Returns** \
[WatcherNotificationKind](../../Bang/Contexts/WatcherNotificationKind.html) \
#### Modified
```csharp
public static const WatcherNotificationKind Modified;
```

Component was modified. It is not called if the entity is dead. Fired whenever the component value is
replaced on the entity, not just when a field within it changes. Maps to
[IReactiveSystem](../../Bang/Systems/IReactiveSystem.html)'s `OnModified` callback.

**Returns** \
[WatcherNotificationKind](../../Bang/Contexts/WatcherNotificationKind.html) \
#### Removed
```csharp
public static const WatcherNotificationKind Removed;
```

Component was removed. Fired even when the removal was caused by the owning entity being destroyed, as
long as the entity previously matched the context. Maps to
[IReactiveSystem](../../Bang/Systems/IReactiveSystem.html)'s `OnRemoved` callback.

**Returns** \
[WatcherNotificationKind](../../Bang/Contexts/WatcherNotificationKind.html) \


⚡
