---
skill: mobile-testing
used_by: [qa-engineer, mobile-engineer]
---

# Mobile (.NET MAUI) Testing

## What's testable without a device/emulator
View models, converters, and any platform-agnostic logic — unit test
these directly, the same way as backend logic.

## What needs a device/emulator
Navigation flows, platform-specific integrations (camera, GPS,
permissions), and visual/layout correctness — test these on at least
one representative device per platform (iOS, Android), not just the
simulator/emulator default.

## Key scenarios to always cover
- Permission denied paths (camera/location refused).
- Offline/poor-connectivity behavior.
- App backgrounding/resuming mid-flow (e.g. mid-form).
- Platform-specific back button behavior (Android) vs. gesture/back
  button (iOS).
