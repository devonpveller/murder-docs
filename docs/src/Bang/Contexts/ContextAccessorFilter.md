# ContextAccessorFilter

**Namespace:** Bang.Contexts \
**Assembly:** Bang.dll

```csharp
public sealed enum ContextAccessorFilter : Enum, IComparable, ISpanFormattable, IFormattable, IConvertible
```

Context accessor filter for a system. This will specify the kind of filter which will be performed on a
certain list of component types. A system declares one or more of these (via
[FilterAttribute](../../Bang/Systems/FilterAttribute.html)) to describe which entities its
[Context](../../Bang/Contexts/Context.html) should track; the [World](../../Bang/World.html) combines
all of a system's filters to decide, entity by entity, whether it belongs in that system's context.

**Implements:** _[Enum](https://learn.microsoft.com/en-us/dotnet/api/System.Enum?view=net-7.0), [IComparable](https://learn.microsoft.com/en-us/dotnet/api/System.IComparable?view=net-7.0), [ISpanFormattable](https://learn.microsoft.com/en-us/dotnet/api/System.ISpanFormattable?view=net-7.0), [IFormattable](https://learn.microsoft.com/en-us/dotnet/api/System.IFormattable?view=net-7.0), [IConvertible](https://learn.microsoft.com/en-us/dotnet/api/System.IConvertible?view=net-7.0)_

### ⭐ Properties
#### AllOf
```csharp
public static const ContextAccessorFilter AllOf;
```

Only entities which has all of the listed components will be fed to the system. An entity must own every
one of the listed component (or message) types to match; this is the most common filter and the default
used by [FilterAttribute](../../Bang/Systems/FilterAttribute.html) when no explicit filter is specified.

**Returns** \
[ContextAccessorFilter](../../Bang/Contexts/ContextAccessorFilter.html) \
#### AnyOf
```csharp
public static const ContextAccessorFilter AnyOf;
```

Filter entities which has any of the listed components will be fed to the system. An entity matches as
soon as it owns at least one of the listed component (or message) types; useful when a system should
react to any member of a family of related components rather than requiring all of them at once.

**Returns** \
[ContextAccessorFilter](../../Bang/Contexts/ContextAccessorFilter.html) \
#### None
```csharp
public static const ContextAccessorFilter None;
```

No filter is required. This won't be applied when filtering entities to a system.
            This is used when a system will, for example, add a new component to an entity but does
            not require such component.

**Returns** \
[ContextAccessorFilter](../../Bang/Contexts/ContextAccessorFilter.html) \
#### NoneOf
```csharp
public static const ContextAccessorFilter NoneOf;
```

Filter out entities that have the components listed. This is typically combined with another filter
(systems may declare multiple [FilterAttribute](../../Bang/Systems/FilterAttribute.html) instances) to
exclude entities that would otherwise match, e.g. entities carrying a "destroyed" or "disabled" marker
component.

**Returns** \
[ContextAccessorFilter](../../Bang/Contexts/ContextAccessorFilter.html) \


⚡
