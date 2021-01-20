---
title: 'Debug hybrid apps - Mobile Blazor Bindings'
---

# Debug hybrid apps

[!INCLUDE [experiment-warning](../includes/experiment-warning.md)]

Debugging hybrid apps poses a challenge because of the mix of native UI components and web UI components.

## Debugging .NET code in hybrid apps

The .NET code (for example, C#) can be debugging via the standard .NET debugging techniques, such as using Visual Studio to debug the app.

## Debugging web UI in hybrid apps

The web UI code in a hybrid app runs in a platform-specific browser view component. These components support various debugging techniques, typically using common browser developer tools.

Common web-specific errors are:

* Missing/incorrect URLs causing resources to not be loaded
* JavaScript interop not working as expected

### Debug Android hybrid web UI

Pre-requisites:

* Have Google Chrome installed on your developer machine

Steps:

1. Launch the affected app in the Android emulator
1. In Google Chrome on your developer machine navigate to `chrome://inspect/#devices`
1. Locate the appropriate "Remote Target" and select the desired inspector, which will then have various debugging options

### Debug iOS hybrid web UI

TODO: Include Safari steps

### Debug Windows hybrid web UI

Steps:

1. Launch the affected app
1. Right-click in any web view in the app and select `Inspect`, which will launch the developer tools

### Debug macOS hybrid web UI

TODO: Include macOS steps

### Debug Tizen hybrid web UI

TODO: Include Tizen steps
