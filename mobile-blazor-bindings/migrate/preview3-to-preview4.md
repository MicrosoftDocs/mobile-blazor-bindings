---
title: 'Migrate Mobile Blazor Bindings From Preview 3 to Preview 4 - Mobile Blazor Bindings'
---

[!INCLUDE [experiment-warning](../includes/experiment-warning.md)]

# Migrate Mobile Blazor Bindings From Preview 3 to Preview 4

This article explains how to update an existing Mobile Blazor Bindings Preview 3 project to Mobile Blazor Bindings Preview 4. If your project is using an earlier preview, please follow the previous migration guides and then proceed to this guide.

For more information see the [announcement blog](https://aka.ms/mbb-preview4-blog) and [release notes](https://aka.ms/mbb-preview4-rel-notes).

## Update NuGet packages to Preview 4 versions

The following NuGet package references need to be updated in all of your solution's projects:

1. `Microsoft.MobileBlazorBindings` version is `0.4.74-preview`
1. `Xamarin.Forms` version is `4.7.0.968` or greater
1. `Xamarin.Essentials` version is `1.5.3.2` or greater (if used in the project)

To update the package versions:

1. Open your application's solution in Visual Studio
1. In Solution Explorer, right-click on the solution node and select "Manage NuGet Packages for Solution."
1. Select the "Updates" tab
1. Ensure that "Include prerelease" is checked
1. Select all applicable packages to update, and ensure that the selected versions match the updated versions listed earlier
1. Click "Update" and go through the proceeding dialogs. This operation can take a few minutes because it will download several NuGet packages and update all the relevant projects.
1. It is recommended to Save All to ensure that all changes to CSPROJ files are committed to disk

You should now be able to build and run your project on this preview.

## Breaking change: Update to .NET Core 3.1

Several new features in Mobile Blazor Bindings Preview 4 require .NET Core 3.1. You will need to install the [.NET Core 3.1 SDK](https://dotnet.microsoft.com/download) to use the new preview.
