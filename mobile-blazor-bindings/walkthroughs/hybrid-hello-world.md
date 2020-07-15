---
title: 'Walkthrough: Hybrid Hello World - Mobile Blazor Bindings'
---

[!INCLUDE [experiment-warning](../includes/experiment-warning.md)]

# Hybrid Hello World - how does it work?

## Introduction

> [!NOTE]
> This page is a continuation of the [Build your first hybrid app](build-first-hybrid-app.md) walkthrough. We recommend you complete that walkthrough before continuing.

> [!TIP]
> For a simpler example, please start with the [Build your first app](build-first-app.md) walkthrough and the subsequent [Hello World Walkthrough](hello-world.md) that show some more basic features of Blazor.

Let's take a look at the initial project that was created in the previous walkthrough to understand more about how to use Experimental Mobile Blazor Bindings for hybrid apps.

The main project to look at is the shared project that contains the `.razor` files. The platform-specific projects contain only minimal code specific to Experimental Mobile Blazor Bindings.

These are the notable files and folders in the shared project:

### Root folder

* `_Imports.razor` - Contains common directives that are applied to all other `.razor` files in this folder and its sub-folders. Sub-folders can have their own `_Imports.razor` files with additional directives. The most common directive type in this file is the `@using` directive, which is used to import a namespace into `.razor` files, exactly the same as a C# `using` statement.
* `App.cs` - Contains the main UI entry point of the application, represented by a class that derives from the [`Xamarin.Forms.Application`](https://docs.microsoft.com/dotnet/api/xamarin.forms.application?view=xamarin-forms) base class. The constructor of this class instantiates a [Generic Host](https://docs.microsoft.com/aspnet/core/fundamentals/host/generic-host?view=aspnetcore-3.0), adds services to the host, and then uses the host to add a Blazor component named `Main` to the main application page. This constructor also registers the main assembly as containing static web resources that are used in the HTML portion of the app. This is where CSS, images, and other resources used by HTML content is located.
* `CounterState.cs` - Contains a service that tracks a counter value and offers related APIs. This service is used in both the native and HTML parts of the app.
* `Main.razor` - Contains the main Blazor UI component of the app. It contains some native UI and also a `BlazorWebView` component that hosts the HTML part of the app.

### WebUI folder

This folder contains the web part of the app. The files and folders here closely match what is found a a Blazor web app.

* `WebUI/_Imports.razor` - Contains common directives for the web part of the app.
* `WebUI/App.razor` - Contains the main entry point for the web part of the app.
* `WebUI/Pages` folder - Contains navigable pages authored using Blazor web syntax. The `.razor` files here all render HTML and share app state with the rest of the app.
* `WebUI/Shared` folder - Contains shared reusable UI components authored using Blazor web syntax. The `.razor` files here all render HTML and are used in other pages in the app. This folder also contains the `MainLayout` component that defines the overall shape of the web part of the app.
* `WebUI/wwwroot` folder - Contains static web assets used in the web part of the app. This is typically CSS files and images. It also contains an `index.html` file that is the container page for the Blazor web UI, and includes references to the CSS files.

Let's dive into the interesting files.

## `App.cs` entry point

The entry point for the app's UI is in this page. It sets up the services for the app and then initializes the UI by attaching a Mobile Blazor Bindings component to the `MainPage` element.

Two sets of services are registered:

1. `services.AddBlazorHybrid()` adds the services required by Mobile Blazor Bindings to host Blazor Web components in the native UI.
1. `services.AddSingleton<CounterState>()` adds an app-specific service that can be consumed from anywhere in the application, including code files, Blazor components, and other services. This is a singleton service, meaning that at most one instance of it will be created, thus allowing the state to be shared.

Learn more about services and DI in the [dependency injection topic](../advanced/dependency-injection.md).

## `Main.razor` native UI page

This is the main native UI page of the app. It contains several native UI components, such as `<Label>` and `<Button>`. It also contains a `<BlazorWebView>` component that hosts the Blazor web content:

```xml
<BlazorWebView ContentRoot="WebUI/wwwroot" VerticalOptions="LayoutOptions.FillAndExpand">
    <FirstBlazorHybridApp.WebUI.App />
</BlazorWebView>
```

A few other interesting things:

* The `<FirstBlazorHybridApp.WebUI.App />` tag is how the native part of the app references the web part of the app.
* The `@inject` directive is used to reference the `CounterState` service.
* The `OnInitialized` and `Dispose` methods are implemented to attach/detach a `StateChanged` event handler so that this UI page refreshes whenever the `CounterState` service indicates that the counter has changed.

## `CounterState.cs` service

This class defines a service that is registered in `App.cs`. It contains state, APIs, and events used to track and report the state of the counter. Various UI components in the app use this service to display their UI and know when to refresh it,

Learn more about services and DI in the [dependency injection topic](../advanced/dependency-injection.md).

## `WebUI/App.razor` web entry point

This file is the main Blazor entry point for the web part of the application. It uses standard Blazor features, such as the [Router](https://docs.microsoft.com/aspnet/core/blazor/fundamentals/routing?view=aspnetcore-3.1). This component determines which Blazor web page to display based on the current route (or show an error if none are found).

## `WebUI/Shared/MainLayout.razor` web layout

Common to most Blazor web apps, this component defines the overall layout of the web part of the app. Here you can include common elements such as navigation, headers, and footers that are used in the web part of the app.

## `WebUI/Pages/Index.razor` web page

Contains a navigable page of web content. The `Index` page is usually the default page that is loaded prior to any navigation

## `WebUI/wwwroot` static web assets folder

This folder contains static web assets used in the web part of the app. That is, these files are served as-is by the web browser component. They are referenced via a relative path within the `wwwroot` folder using standard web/HTML/CSS patterns (such as `<img src="images/header.png" ...>` for a file `WebUI/wwwroot/images/header.png`).

These files get embedded in the application and are handled by Mobile Blazor Bindings automatically. Files in this folder can be read from code by calling `BlazorHybridHost.TryGetEmbeddedResourceFile("file_name", out var stream)`, as seen in the app's `WebUI/Pages/FetchData.razor` file.

Assemblies containing static web assets must be registered by calling `BlazorHybridHost.AddResourceAssembly(GetType().Assembly, contentRoot: "WebUI/wwwroot");`, as seen in the app's `App.cs` file.

This project contains the Bootstrap CSS library to provide styles for common UI scenarios.

## Other files

We encourage you to explore all the files in the application to learn their contents and how they interact.
