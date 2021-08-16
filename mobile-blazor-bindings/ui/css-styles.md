---
title: 'CSS Styles - Mobile Blazor Bindings'
ms.topic: article
ms.prod: aspnet-core
---

# CSS Styles

[!INCLUDE [experiment-warning](../includes/experiment-warning.md)]

## Overview

Applications built using Mobile Blazor Bindings have an assortment of styles that can be applied to control the appearance of the UI. These styles can be applied directly to components or they can be applied using Cascading Style Sheets (CSS). Some of the advantages of using CSS instead of direct styles is that it enables better separation of concerns (that is, keeping component styles separate from their layout and functionality) and allowing possible sharing of CSS with other media (for example, a web app).

## Including CSS in a project

To add CSS to a Mobile Blazor Bindings project:

1. In the shared UI project of your application right-click on any folder and select Add --> Add New Item and select the Style Sheet item type (if you can't find it, use the search feature to find `style sheet`).
1. Choose an appropriate name for your style sheet and press Add.
1. Edit the contents of the CSS file as needed (see below for supported styles). For example, to set all labels to have a `large` font size:

    ```css
    label {
        font-size: large;
    }
    ```

1. Open the `.razor` file where you want to use the CSS.

   > [!NOTE]
   > Many apps will have a single CSS file that is included in the main page of the application.

1. Add the following markup to the `.razor` file, typically at the top level of the file. Changing the name and path of the CSS file to match what you created:

    ```xml
    <StyleSheet Resource="folder/MyStyles.css" Assembly="GetType().Assembly"></StyleSheet>
    ```

> [!NOTE]
> CSS support requires referencing Xamarin.Forms 4.5 or newer. To update this reference, manage the NuGet packages for the solution and ensure that the solution is using a version of Xamarin.Forms that is 4.5 or newer. Future versions of Mobile Blazor Bindings will include this version by default.

## Applying CSS to components

CSS styles are declared in the CSS file using standard CSS syntax. Styles are specified using selectors, which allow applying styles based on element type, base class, name, class attribute, and several other means (see below for Xamarin.Forms reference).

In the `.razor` file on each component that allows CSS styles you can set the class or name via the `class` and `StyleId` properties, respectively.

> [!NOTE]
> Elements that support CSS styles also have a `StyleClass` property, which is equivalent to the `class` property. If you need to use the `class` property programmatically from C#, either use the escape syntax `@class`, such as `myElement.@class`, or use the `StyleClass` property, such as `myElement.StyleClass`.

Example CSS file:

```css
/* this rule applies to all labels */
label {
    font-size: large;
}

/* these rules apply only when this class is specified */
.happyText {
    color: green;
}

.sadText {
    color: red;
}
```

Example Razor file snippet:

```xml
<Label Text="Seattle" /> @* no class specified, so only 'label' rule applied *@
<Label class="happyText" Text="Weather: good" /> @* class is specified, so 'label' rule and '.happyText' rules applied *@
<Label class="sadText" Text="Traffic: bad" /> @* class is specified, so 'label' rule and '.sadText' rules applied *@
```

## Supported CSS styles

Because the built-in UI components are based on Xamarin.Forms controls, refer to [Styling Xamarin.Forms apps using CSS](https://docs.microsoft.com/xamarin/xamarin-forms/user-interface/styles/css/) to learn more about this feature and which styles can be applied to which components.

## Troubleshooting

### Set Build Action to Embedded resource

When adding a new CSS file in Visual Studio, the CSS file should automatically have its `Build Action` set to `Embedded resource` to ensure it is included in the built project. If it isn't, right-click on the CSS file, select Properties, and set `Build Action` to `Embedded resource`.

### Use correct path syntax for CSS in sub-folders

If the CSS file is located in a folder, specify its name using its path with forward-slashes as the path separators. For example, if the CSS file is `<PROJECT ROOT>/assets/styles/MyApp.css`, then the markup to include it in a `.razor` file is:

```xml
<StyleSheet Resource="assets/styles/MyApp.css" Assembly="GetType().Assembly"></StyleSheet>
```
