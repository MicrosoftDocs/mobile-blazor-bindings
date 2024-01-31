---
title: 'Migrate Mobile Blazor Bindings From Preview 4 to Preview 5 - Mobile Blazor Bindings'
ms.topic: article
ms.service: aspnet-core
---

# Migrate Mobile Blazor Bindings From Preview 4 to Preview 5

[!INCLUDE [experiment-warning](../includes/experiment-warning.md)]

This article explains how to update an existing Mobile Blazor Bindings Preview 4 project to Mobile Blazor Bindings Preview 5. If your project is using an earlier preview, follow the previous migration guides and then proceed to this guide.

For more information see the [announcement blog](https://aka.ms/mbb-preview5-blog) and [release notes](https://aka.ms/mbb-preview5-rel-notes).

## Update NuGet packages to Preview 5 versions

The following NuGet package references need to be updated in all of your solution's projects:

1. `Microsoft.MobileBlazorBindings` version is `0.5.50-preview`
1. `Xamarin.Forms` version is `4.8.0.1451` or greater
1. `Xamarin.Essentials` version is `1.5.3.2` or greater (if used in the project)
1. `Microsoft.Web.WebView2` - remove direct references to this package (from the Windows project) because it will be picked up transitively

To update the package versions:

1. Open your application's solution in Visual Studio
1. In Solution Explorer, right-click on the solution node and select "Manage NuGet Packages for Solution."
1. Select the "Updates" tab
1. Ensure that "Include prerelease" is checked
1. Select all applicable packages to update, and ensure that the selected versions match the updated versions listed earlier
1. Click "Update" and go through the proceeding dialogs. This operation can take a few minutes because it will download several NuGet packages and update all the relevant projects.
1. It is recommended to Save All to ensure that all changes to CSPROJ files are committed to disk

You should now be able to build and run your project on this preview.

## Non-hybrid app migration

For non-hybrid apps the steps above cover the major changes regarding versions. The main other change is related to Grid layout syntax, which you can find below.

## Hybrid app migration

A Blazor Hybrid app created with Mobile Blazor Bindings Preview 4 requires several changes to update to Preview 5. The simplest way to migrate is to create a new project using Preview 5 and copying over all customizations.

To see all the changes in the default templates refer to [Changes from Preview 4 v0.4.74-preview to Preview 5 v0.5.50-preview](https://github.com/Eilon/MobileBlazorBindingsMigration/compare/v0.4.74-preview...v0.5.50-preview)

If you want to make the changes individually, follow these steps:

1. In the shared UI project:
    1. Move the `wwwroot` folder that contains static web assets to the root of the project (it used to be a sub-folder of the `WebUI` folder)
    1. In `Main.razor` remove the `ContentRoot` property from the `<BlazorWebView>` control
    1. In `App.cs` change the constructor to match this code (while preserving any customizations you have made, such as registering app-specific services):

        ```csharp
        public App(IFileProvider fileProvider = null)
        {
            var hostBuilder = MobileBlazorBindingsHost.CreateDefaultBuilder()
                .ConfigureServices((hostContext, services) =>
                {
                    // Adds web-specific services such as NavigationManager
                    services.AddBlazorHybrid();

                    // Register app-specific services
                    services.AddSingleton<CounterState>();
                })
                .UseWebRoot("wwwroot");

            if (fileProvider != null)
            {
                hostBuilder.UseStaticFiles(fileProvider);
            }
            else
            {
                hostBuilder.UseStaticFiles();
            }
            var host = hostBuilder.Build();

            MainPage = new ContentPage { Title = "My Application" };
            host.AddComponent<Main>(parent: MainPage);
        }
        ```

    1. In the CSPROJ file remove the `<WwwRootResourcePath>` element and remove the `<EmbeddedResource ... />` element that references it. (The project should no longer mention `WwwRootResourcePath` at all).
    1. If the project has code that reads a static file in the project (such as the default template's `WebUI/Pages/FetchData.razor` file), do the following instead:
        1. Inject the file provider service by adding `@inject Microsoft.Extensions.FileProviders.IFileProvider FileProvider` to the `.razor` file
        1. Try to open the file and read it by calling:

            ```csharp
            var fileInfo = FileProvider.GetFileInfo("_content/PROJECT_NAME/filename.json");
            if (fileInfo != null && fileInfo.Exists)
            {
                using (var stream = fileInfo.CreateReadStream())
                {
                    var data = await JsonSerializer.DeserializeAsync<DATA_TYPE>(stream, ...);
                }
            }
            ```

1. For Android:
    1. In `MainActivity.cs` add a constructor argument to the `App` constructor: `LoadApplication(new App(new AssetFileProvider(Assets, "wwwroot")));`. Import any required namespaces, such as `Microsoft.MobileBlazorBindings.WebView.Android`.
    1. Create a folder in the Android project called `wwwroot` folder and copy the `wwwroot/index.html` file from the shared UI project there. Then right-click on the file and select Properties. Set its Build Action to `None` and set `Copy if newer`.
1. For iOS:
    1. Create a folder in the iOS project called `Resources/wwwroot` folder and copy the `wwwroot/index.html` file from the shared UI project there. Then right-click on the file and select Properties. Ensure that the Build Action is set to `Content`.
1. For macOS:
    1. Create a folder in the macOS project called `Resources/wwwroot` folder and copy the `wwwroot/index.html` file from the shared UI project there. Then right-click on the file and select Properties. Ensure that the Build Action is set to `Content`.
1. For Windows:
    1. Create a folder in the Windows project called `wwwroot` folder and copy the `wwwroot/index.html` file from the shared UI project there. Then right-click on the file and select Properties. Ensure that the Build Action is set to `Content` and set `Copy if newer`.
1. After completing the previous steps, you can go back to the shared UI project and delete `wwwroot/index.html` because it is now in the platform-specific projects

## Breaking change: Grid syntax change for row and column definitions

The Grid control's syntax for row and column definitions has been simplified:

1. Remove the `<Layout>` and `<Contents>` sections from the `<Grid>` control
1. Have the grid's row and column definitions defined as comma-separated strings instead of as individual collection items

In Preview 4 and earlier the Grid had `<Layout>` and `<Contents>` sections, and multiple `<RowDefinition>`/`<ColumnDefinition>` items:

```xml
<Grid VerticalOptions="LayoutOptions.FillAndExpand">
    <Layout>
        <RowDefinition GridUnitType="GridUnitType.Auto" />
        <RowDefinition GridUnitType="GridUnitType.Auto" />
        <RowDefinition GridUnitType="GridUnitType.Auto" />
        <ColumnDefinition GridUnitType="GridUnitType.Auto" />
        <ColumnDefinition GridUnitType="GridUnitType.Auto" />
    </Layout>
    <Contents>
        <GridCell Row="0" Column="0" ColumnSpan="2">
            <Label BackgroundColor="Color.LightBlue" Text="Todo items" FontSize="20" />
        </GridCell>
        <GridCell Row="1" Column="0">
            <Switch IsToggled="true" />
        </GridCell>
        <GridCell Row="1" Column="1">
            <Label Text="Use awesome Xamarin.Forms features" FontSize="20" />
        </GridCell>
        <GridCell Row="2" Column="0">
            <Switch IsToggled="true" />
        </GridCell>
        <GridCell Row="2" Column="1">
            <Label Text="Delight our customers" FontSize="20" />
        </GridCell>
    </Contents>
</Grid>
```

Starting in Preview5 the `<Layout>` and `<Content>` sections are removed, and all row/column definitions are specified as strings (9 lines of markup REMOVED!):

```xml
<Grid VerticalOptions="LayoutOptions.FillAndExpand" RowDefinitions="Auto, Auto, Auto" ColumnDefinitions="Auto, Auto">
    <GridCell Row="0" Column="0" ColumnSpan="2">
        <Label BackgroundColor="Color.LightBlue" Text="Todo items" FontSize="20" />
    </GridCell>
    <GridCell Row="1" Column="0">
        <Switch IsToggled="true" />
    </GridCell>
    <GridCell Row="1" Column="1">
        <Label Text="Use awesome Xamarin.Forms features" FontSize="20" />
    </GridCell>
    <GridCell Row="2" Column="0">
        <Switch IsToggled="true" />
    </GridCell>
    <GridCell Row="2" Column="1">
        <Label Text="Delight our customers" FontSize="20" />
    </GridCell>
</Grid>
```

For more Grid information, refer to the [Grid Layout](../ui/grid-layout.md) topic.
