---
title: 'Components Reference - Mobile Blazor Bindings'
---

[!INCLUDE [experiment-warning](../includes/experiment-warning.md)]

# Components Reference

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

To learn more about Blazor and Razor syntax, please refer to the [References](../advanced/references.md) topic.

## UI component categories

The built-in components can be divided into several broad categories:

1. Pages. These components occupy all or most of a screen.
1. Layouts. These components are containers for views and other layouts.
1. Views. These components are user-interface objects such as labels, buttons, and sliders.
1. Other specialized components, such as the Application object, Span (for formatted text), and menu items.

## Built-in components

1. Page components
   * ContentPage
   * MasterDetailPage
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
   * Button
   * ActivityIndicator
   * Image
   * Entry
   * Label
   * Stepper
   * Switch

1. Specialized components
   * Application
   * BaseMenuItem
   * FormattedString
   * GestureElement
   * MenuItem
   * Shell (including ShellContent, ShellGroupItem, ShellItem, FlyoutItem, TabBar, ShellSection, Tab)
   * Span

## More information

Because the built-in UI components are based on Xamarin.Forms controls, you can refer to the [Xamarin.Forms Controls Reference](https://docs.microsoft.com/xamarin/xamarin-forms/user-interface/controls/) to learn more about how they work and their properties and events.
