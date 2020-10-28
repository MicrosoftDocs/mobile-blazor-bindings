---
title: 'Migrate Mobile Blazor Bindings From Preview 4 to Preview 5 - Mobile Blazor Bindings'
---

# Migrate Mobile Blazor Bindings From Preview 4 to Preview 5

[!INCLUDE [experiment-warning](../includes/experiment-warning.md)]

This article explains how to update an existing Mobile Blazor Bindings Preview 4 project to Mobile Blazor Bindings Preview 5. If your project is using an earlier preview, follow the previous migration guides and then proceed to this guide.

For more information see the [announcement blog](https://aka.ms/mbb-preview5-blog) and [release notes](https://aka.ms/mbb-preview5-rel-notes).

## Update NuGet packages to Preview 5 versions

The following NuGet package references need to be updated in all of your solution's projects:

1. `Microsoft.MobileBlazorBindings` version is `0.4.TODO`
1. `Xamarin.Forms` version is `TODO` or greater
1. `Xamarin.Essentials` version is `TODO` or greater (if used in the project)

To update the package versions:

1. Open your application's solution in Visual Studio
1. In Solution Explorer, right-click on the solution node and select "Manage NuGet Packages for Solution."
1. Select the "Updates" tab
1. Ensure that "Include prerelease" is checked
1. Select all applicable packages to update, and ensure that the selected versions match the updated versions listed earlier
1. Click "Update" and go through the proceeding dialogs. This operation can take a few minutes because it will download several NuGet packages and update all the relevant projects.
1. It is recommended to Save All to ensure that all changes to CSPROJ files are committed to disk

You should now be able to build and run your project on this preview.

## Breaking change: TODO

TODO

## TODO: Another change

TODO
