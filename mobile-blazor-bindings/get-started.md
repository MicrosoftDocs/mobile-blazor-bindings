---
title: 'Creating an app with Mobile Blazor Bindings - Mobile Blazor Bindings'
ms.topic: article
ms.prod: aspnet-core
---

# Creating an app with Experimental Mobile Blazor Bindings

[!INCLUDE [experiment-warning](includes/experiment-warning.md)]

Creating an app involves a few steps:

1. Create a new Experimental Mobile Blazor Bindings mobile app project from the `dotnet new` templates
1. Open the new project in an editor such as Visual Studio
1. Write your app
1. Run it!

## Prerequisites

Experimental Mobile Blazor Bindings requires the following software:

1. [.NET Core 3.1 SDK](https://dotnet.microsoft.com/download)
1. Visual Studio or Visual Studio for Mac, with the following workloads installed:
   * Mobile development with .NET (Xamarin.Forms)
   * ASP.NET and web development
1. Additional requirements to build and run Blazor Hybrid Apps:
   * On Windows: install [Microsoft Edge Canary Channel](https://www.microsoftedgeinsider.com/download)
   * On Mac: no additional requirements

## Install the project templates

1. Open a command prompt or shell window
1. Install the Experimental Mobile Blazor Bindings project templates by running this command:

    ```shell
    dotnet new -i Microsoft.MobileBlazorBindings.Templates::0.5.50-preview
    ```

## Next steps

You're now ready to [build your first app](walkthroughs/build-first-app.md) or [build your first hybrid app](walkthroughs/build-first-hybrid-app.md)!
