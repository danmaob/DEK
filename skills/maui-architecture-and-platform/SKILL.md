---
skill: maui-architecture-and-platform
used_by: [mobile-engineer]
---

# .NET MAUI Architecture & Platform Integration

## MVVM
Use MVVM for screens with real interactive state (forms, lists with
actions, anything with commands); a static/informational screen can
stay code-behind-light without a full view model. Bind data with
`INotifyPropertyChanged` (or a source-generator based implementation)
rather than manually pushing values into controls.

## Navigation
Centralize navigation logic (e.g. Shell navigation) rather than
scattering `Navigation.PushAsync` calls with hardcoded routes through
view models.

## Platform-specific behavior
Isolate platform differences behind an abstraction
(`partial` classes, dependency-injected platform services) rather than
`#if ANDROID`/`#if IOS` scattered through shared code.

## Permissions & device features
Request permissions (camera, location) just before the feature that
needs them, handle denial gracefully with a clear explanation, and
never assume a permission granted once stays granted (the OS can
revoke it).

## Local storage & connectivity
Use secure storage for sensitive data (tokens), never plain
preferences/files. Check `Connectivity.NetworkAccess` before
network-dependent actions and degrade gracefully when offline.
