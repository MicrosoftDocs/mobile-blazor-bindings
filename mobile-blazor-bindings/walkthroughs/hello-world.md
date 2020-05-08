---
title: 'Walkthrough: Hello World - Mobile Blazor Bindings'
---

[!INCLUDE [experiment-warning](../includes/experiment-warning.md)]

# Hello World - how does it work?

## Introduction

> [!NOTE]
> This page is a continuation of the [Build your first app](build-first-app.md) walkthrough. We recommend you complete that walkthrough before continuing.

Let's take a look at the initial project that was created in the previous walkthrough to understand more about how to use Experimental Mobile Blazor Bindings.

The main project to look at is the shared project that contains the `.razor` files. The Android and iOS projects don't contain any code specific to Experimental Mobile Blazor Bindings.

These are the files in the shared project:

* `_Imports.razor` - Contains common directives that are applied to all other `.razor` files in this folder and its sub-folders. Sub-folders can have their own `_Imports.razor` files with additional directives. The most common directive type in this file is the `@using` directive, which is used to import a namespace into `.razor` files, exactly the same as a C# `using` statement.
* `App.cs` - Contains the main UI entry point of the application, represented by a class that derives from the [`Xamarin.Forms.Application`](https://docs.microsoft.com/dotnet/api/xamarin.forms.application?view=xamarin-forms) base class. The constructor of this class instantiates a [Generic Host](https://docs.microsoft.com/aspnet/core/fundamentals/host/generic-host?view=aspnetcore-3.0), adds services to the host (the default project has none), and then uses the host to add a Blazor component named `HelloWorld` to the application element (`this`).
* `Counter.razor` - Contains a Blazor Component named `Counter`.
* `HelloWorld.razor` - Contains a Blazor Component named `HelloWorld`.

Let's dive into the two Blazor Components to see how they work.


## Counter Blazor Component

This component contains two sections:

1. The markup that defines the UI elements and their associated properties and event handlers:

    ```xml
    <Frame CornerRadius="10" BackgroundColor="Color.LightBlue">

        <StackLayout Orientation="StackOrientation.Horizontal" HorizontalOptions="LayoutOptions.Center">

            <Button Text="Increment" OnClick="IncrementCount" />

            <Label Text="@("The button was clicked " + count + " times")"
                FontAttributes="FontAttributes.Bold"
                VerticalTextAlignment="TextAlignment.Center" />

        </StackLayout>

    </Frame>
    ```

    The HTML-like tags represent UI components that match the Xamarin.Forms components and their properties and events. Some properties have computed values, such as the `Label` component's `Text` property, which has its value set to a value computed by C# code, which is denoted by the `@( ... )` expression block.

    When an event handler is run, such as the `Button` component's `OnClick` event, the component automatically re-renders, which enables the UI to update without any additional logic. More advanced scenarios can control which components re-render and when.

2. The code that implements any event handlers or other component functionality, wrapped in an `@code { ... }` block:

    ```c#
    int count;

    void IncrementCount()
    {
        count++;
    }
    ```

    This code increments the `count` field, which is also used as the computed value of the `Label` component's `Text` property. After the `IncrementCount()` event handler is run, the new value of `count` will be used when the UI re-renders.


## HelloWorld Blazor Component

The HelloWorld component contains only markup:

```xml
<ContentView>
    <StackLayout Margin="new Thickness(20)">

        <Label Text="Hello, World!"
               FontSize="40" />

        <Counter />

    </StackLayout>
</ContentView>
```

Note that the `Counter` component is referenced in this component by referencing it as a tag `<Counter />`.

Every Blazor Component is compiled into a class with the same name as the file. The namespace is the root namespace of the project, plus the folder names, if any, separated by dots (`.`). The type can be referenced by other C# code via its type name (not common), or in a `.razor` file by using it as a tag.
