---
title: 'Custom components - Mobile Blazor Bindings'
---

[!INCLUDE [experiment-warning](../includes/experiment-warning.md)]

# Custom components

You can write reusable custom components either using Blazor components or by wrapping existing Xamarin.Forms components.

## Blazor components

You can create a reusable Blazor component by writing a `.razor` file just like you would in an application. The component can be shipped as a NuGet package so that it is easily reusable in other projects.

To learn more about component libraries, check out the [ASP.NET Core Razor components class libraries](https://docs.microsoft.com/aspnet/core/blazor/class-libraries?view=aspnetcore-3.1&tabs=visual-studio).

More details coming soon!

## Wrapping Xamarin.Forms components

To make a Xamarin.Forms element available in Blazor markup you need to implement two types of classes:

1. A component representing the markup that the developer will use in the `.razor` file. This type will need to derive from `NativeControlComponentBase` or one of its derived classes.
1. An element handler representing the UI component that will be created when the component is used. This type will either implement the `IXamarinFormsElementHandler` interface or derive from one of the existing handler types that implement the interface.

An example that shows how to wrap the popular [`PancakeView` component](https://github.com/sthewissen/Xamarin.Forms.PancakeView) is available [here](https://github.com/xamarin/MobileBlazorBindings/tree/master/samples/MobileBlazorBindingsWeather/Microsoft.MobileBlazorBindings.PancakeView).

The component uses a static constructor to register the component mapping to the element handler, as seen [here](https://github.com/xamarin/MobileBlazorBindings/blob/master/samples/MobileBlazorBindingsWeather/Microsoft.MobileBlazorBindings.PancakeView/Elements/PancakeView.cs#L11-L15).
