---
title: 'Migrate Mobile Blazor Bindings From Preview 2 to Preview 3 - Mobile Blazor Bindings'
---

[!INCLUDE [experiment-warning](../includes/experiment-warning.md)]

# Migrate Mobile Blazor Bindings From Preview 2 to Preview 3

This article explains how to update an existing Mobile Blazor Bindings Preview 2 project to Mobile Blazor Bindings Preview 3. If your project is using Preview 1, please migrate to Preview 2 using the [previous migration guide](preview1-to-preview2.md), and then proceed to this guide.

For more information see the [announcement blog](https://aka.ms/mbb-preview3-blog) and [release notes](https://aka.ms/mbb-preview3-rel-notes).

## Update NuGet packages to Preview 3 versions

The following NuGet package references need to be updated in all of your solution's projects:

1. `Microsoft.MobileBlazorBindings` version is 0.3.26-preview
1. `Xamarin.Forms` version is 4.5.0.356 or greater
1. `Xamarin.Essentials` version is 1.5.0 or greater (if used in the project)

To update the package versions:

1. Open your application's solution in Visual Studio
1. In Solution Explorer, right-click on the solution node and select "Manage NuGet Packages for Solution."
1. Select the "Updates" tab
1. Ensure that "Include prerelease" is checked
1. Select all applicable packages to update, and ensure that the selected versions match the updated versions listed earlier
1. Click "Update" and go through the proceeding dialogs. This operation can take a few minutes because it will download several NuGet packages and update all the relevant projects.
1. It is recommended to Save All to ensure that all changes to CSPROJ files are committed to disk

You should now be able to build and run your project on this preview.

## Breaking change: 'class' and 'StyleClass' properties use spaces as separators

The `class` and `StyleClass` properties were changed to use spaces as separators instead of commas. This change was made so that the syntax matches the HTML syntax for specifying CSS classes.

Before (with comma separators):

```xml
<Label class="successText, bannerText" Text="You win!" />
```

After (with space separators):

```xml
<Label class="successText bannerText" Text="You win!" />
```

## Changes to Label component syntax (remove certain tags, inline text)

While most `<Label>` components use the `Text="abc"` property, the `<Label>` component also has an optional syntax where you can define complex strings as a sequence of string spans, each with its own styles. The syntax for the `<Label>` component has been simplified to remove unnecessary tags for complex strings and create cleaner markup.

There are two changes for this improvement:

1. A `<Span>` tag's `Text` property can be set inline instead of as a property.
1. The `<FormattedText>`, `<FormattedString>`, and `<Spans>` tags are no longer used.

Before (with many tags and using the `Text` property):

```xml
<Label FontSize="12">
    <FormattedText>
        <FormattedString>
            <Spans>
                <Span Text="This text is large... " FontSize="50" />
                <Span Text="and this is plain... " />
                <Span Text="and this is green!"
                        TextColor="Color.Green" />
            </Spans>
        </FormattedString>
    </FormattedText>
</Label>
```

After (with fewer tags and using inline text):

```xml
<Label FontSize="12">
    <Span FontSize="50">This text is large... </Span>
    <Span>and this is plain... </Span>
    <Span TextColor="Color.Green">and this is green!</Span>
</Label>
```

## Optional: Use inner text of Button instead of Text property

The `<Button>` component now allows setting the `Text` property via inline text in addition to setting the `Text` property. This change is optional and both syntaxes are supported.

Before (using the `Text` property, still works):

```xml
<Button Text="Hello, world!" />
```

After (using inline text):

```xml
<Button>Hello, world!</Button>
```
