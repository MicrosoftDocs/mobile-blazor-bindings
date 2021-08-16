---
title: 'Components Reference - Mobile Blazor Bindings'
ms.topic: article
ms.prod: aspnet-core
---

# Components Reference

[!INCLUDE [experiment-warning](../includes/experiment-warning.md)]

## Overview

Applications built using Mobile Blazor Bindings are constructed using UI components. UI components can come from the built-in libraries, 3rd parties, or you can write your own. To author custom components, refer to the [Custom Components](../advanced/custom-components.md) topic.

UI components are used by referencing them with standard Razor syntax. For example:

```xml
<SomeComponent
    Property1="value1"
    Property2="@variable2">
    ... possibly some inner content ...
</SomeComponent>>
```

To learn more about Blazor and Razor syntax, refer to the [References](../advanced/references.md) topic.

## UI component categories

The built-in components can be divided into several broad categories:

1. Pages. These components occupy all or most of a screen.
1. Layouts. These components are containers for views and other layouts.
1. Views. These components are user-interface objects such as labels, buttons, and sliders.
1. Other specialized components, such as the Application object, Span (for formatted text), and menu items.

## Built-in components

1. Page components
   * ContentPage
   * FlyoutPage
   * Page
   * TabbedPage
   * TemplatedPage

1. Layout components
   * ContentView
   * Frame
   * Grid
   * ScrollView
   * StackLayout

1. View components
   * ActivityIndicator
   * BoxView
   * Button
   * CheckBox
   * DatePicker
   * Image
   * ImageButton
   * Entry
   * Label
   * ProgressBar
   * Slider
   * Stepper
   * Switch
   * TimePicker

1. Specialized components
   * Application
   * BaseMenuItem
   * BlazorWebView
   * FormattedString
   * GestureElement
   * MenuItem
   * Shell (including ShellContent, ShellGroupItem, ShellItem, FlyoutItem, TabBar, ShellSection, Tab)
   * Span
   * StyleSheet
   * WebView

## More information

Because most of the built-in UI components are based on Xamarin.Forms controls, you can refer to the [Xamarin.Forms Controls Reference](https://docs.microsoft.com/xamarin/xamarin-forms/user-interface/controls/) to learn more about how they work and their properties and events.
