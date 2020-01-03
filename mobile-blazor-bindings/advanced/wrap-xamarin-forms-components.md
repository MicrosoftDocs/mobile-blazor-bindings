---
title: 'Wrap Xamarin.Forms components'
---

# Wrap Xamarin.Forms components

To make a Xamarin.Forms element available in Blazor markup you need to implement two types of classes:

1. A component representing the markup that the developer will use in the `.razor` file
1. An element handler representing the UI component that will be created when the component is used

An example that shows how to wrap the popular [`PancakeView` component](https://github.com/sthewissen/Xamarin.Forms.PancakeView) is available [here](https://github.com/xamarin/Emblazon/tree/master/samples/MobileBlazorBindingsWeather/Microsoft.MobileBlazorBindings.PancakeView).

The component uses a static constructor to register the component mapping to the element handler, as seen [here](https://github.com/xamarin/Emblazon/blob/master/samples/MobileBlazorBindingsWeather/Microsoft.MobileBlazorBindings.PancakeView/Elements/PancakeView.cs#L11-L15).
