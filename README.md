# Nexora Browser

A native C++ browser shell project for Nexora OS.

## Current status

This repository starts the **native browser application layer**: toolbar, address entry, navigation history, bookmarks, downloads view, keyboard shortcuts, and profile-storage integration points.

It is **not yet a functioning general-purpose web browser**. Nexora OS still needs a user-mode networking API (DNS/TCP), TLS with certificate verification, HTTP, and a compatible HTML/CSS/JavaScript engine. The app must never pretend a URL loaded when it did not.

## Product direction

- Quiet, polished desktop UI: charcoal surfaces, restrained silver accents, clear hierarchy, no decorative AI cards or fake metrics.
- Keyboard-first navigation and responsive layouts.
- Local profile data by default, with storage behind a profile adapter so it can be connected to the real Nexora OS account/profile service.
- Downloads must use streaming writes, safe filename handling, cancellation, and explicit destination selection.
- Security before compatibility: verified TLS certificates, origin isolation, sandboxing, and no silent certificate bypass.

## Source layout

- `user/apps/browser/browser.cpp` — native app shell for the Nexora OS `hzui` API.
- `rootfs/Nexora/Apps/browser.app` — OS application manifest.
- `docs/ENGINE_PORT.md` — engine and networking port plan.

## Integration

Copy the source and manifest into the matching paths in the Nexora OS tree, then use the OS repository's normal build and QEMU test workflow. This repository alone does not contain the Nexora OS SDK or kernel headers, so it cannot be built independently here.

## Engine strategy

See [docs/ENGINE_PORT.md](docs/ENGINE_PORT.md). A mature engine port is preferable to writing a JavaScript engine or TLS stack from scratch. A source drop is not a port: the engine needs platform threading, memory, graphics, font, network, storage, and sandbox adapters, and its license must be respected.
