---
title: 'Experimental Tizen Support for Mobile Blazor Bindings'
---

# Experimental Tizen Support

[!INCLUDE [experiment-warning](../includes/experiment-warning.md)]

To get started building Mobile Blazor Bindings native and hybrid applications for Tizen use these samples as a starting point:

* [Blazor Hybrid app with Tizen](https://github.com/xamarin/MobileBlazorBindings/tree/master/samples/HybridApp/HybridApp.Tizen)
* [Blazor Hybrid app with Tizen and auth](https://github.com/xamarin/MobileBlazorBindings/tree/master/samples/HybridAuthSample/HybridAuthApp.Tizen)

## Prerequisites

Building Tizen applications requires the Tizen SDK, emulators, and their dependencies. Learn more at the [Tizen .NET documentation](https://docs.microsoft.com/xamarin/xamarin-forms/platform/other/tizen) and how to [install the developer tools](https://developer.tizen.org/development/tizen-extensions-visual-studio-family) for Visual Studio and Visual Studio for Mac.

## Known issues

The following is a list of known issues in the preview of Tizen support for Mobile Blazor Bindings:

* Tizen application startup code in the project's `Main.cs` has to re-register the WebView renderer and set up custom loading of assemblies.
* Static assets used in a BlazorWebView must be directly included in the Tizen project. They are not automatically copied and embedded from the shared UI project.
* There are no project templates for Tizen at this time.

## Troubleshooting

TODO
