---
title: 'Build from Source - Mobile Blazor Bindings'
ms.topic: article
ms.prod: aspnet-core
---

# Build from Source

[!INCLUDE [experiment-warning](../includes/experiment-warning.md)]

> [!NOTE]
> These instructions are Windows-only, but suitable alternatives should work on other operating systems.

1. Clone the repo from <https://github.com/xamarin/MobileBlazorBindings>
1. Open a Visual Studio Developer Command Prompt window
1. Navigate to the repo root
1. Run `init.cmd` from the command line to install required assets (a one-time operation)
1. Run `msbuild` to build all projects
1. Run `pack.cmd` to produce NuGet packages. The output will be in the repo root's `bin` directory.
1. You can now copy these packages to a local folder and use that local folder as a NuGet package feed in the NuGet Package Manager or `NuGet.config` file.
