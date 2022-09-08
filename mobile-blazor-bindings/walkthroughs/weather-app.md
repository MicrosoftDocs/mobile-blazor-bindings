---
title: 'Walkthrough: Weather App - Mobile Blazor Bindings'
ms.topic: tutorial
ms.prod: aspnet-core
---

# Weather App

[!INCLUDE [experiment-warning](../includes/experiment-warning.md)]

The completed Weather app sample is available [here](https://github.com/xamarin/MobileBlazorBindings/tree/master/samples/MobileBlazorBindingsWeather). The sample uses a 3rd party Xamarin.Forms component, the `Grid` component, two-way bindings, component initialization logic, dependency injection, CSS styles, and many more features.

The completed app looks like this:

[ ![Weather App running in the Android Emulator](./media/weather-app/weather-app-inline.png) ](./media/weather-app/weather-app-expanded.png#lightbox)

Rather than write the app from scratch, let's take a look at the key components in this sample application.

1. `Grid` component. The entire UI of the Weather App is contained in the [`WeatherApp` component](https://github.com/xamarin/MobileBlazorBindings/blob/master/samples/MobileBlazorBindingsWeather/MobileBlazorBindingsWeather/WeatherApp.razor), with its main layout established by a `Grid` component.

   * The `Grid` component has two main sections to establish its structure: the row/column definitions and the grid cells

        ```xml
        <Grid RowDefinitions="..." ColumnDefinitions="...">
            @* GridCell components *@
        </Grid>
        ```

   * The `RowDefinition` and `ColumnDefinition` properties establish the structure of the grid:

        ```xml
        RowDefinitions="Auto, *, Auto, Auto, Auto, Auto, Auto"
        ```

     The properties are optional and if they are omitted imply a single row/column. Each comma-separated value specifies the relative, absolute, or automatic dimensions of that row/column.

     Learn more about the properties here:

        * [ColumnDefinition](/dotnet/api/xamarin.forms.columndefinition)
        * [RowDefinition](/dotnet/api/Xamarin.Forms.RowDefinition)

   * The content of the Grid contains several `<GridCell>` components that can have a `Row`, `Column`, `RowSpan`, and `ColumnSpan` property, and contain a single item representing the cells contents. All of these properties are optional. For example, this `GridCell` will be on row index 6, column index 0, and no row/column span:

        ```xml
        <GridCell Row="6">
            <StackLayout Orientation="StackOrientation.Horizontal"
                        HorizontalOptions="LayoutOptions.Center">
                <Label Text="I'm feeling too hot/cold!"
                        VerticalOptions="LayoutOptions.Center"/>
                <Stepper @bind-Value="Temperature"
                            Minimum="0"
                            Maximum="120"
                            Increment="3"
                            Opacity="0.6"
                            VerticalOptions="LayoutOptions.Center" />
            </StackLayout>
        </GridCell>
        ```

1. A popular 3rd party component often used in Xamarin.Forms apps is the [`PancakeView` component](https://github.com/sthewissen/Xamarin.Forms.PancakeView). The component has been wrapped to enable it to be used with Blazor syntax in a separate class library project: [Microsoft.MobileBlazorBindings.PancakeView](https://github.com/xamarin/MobileBlazorBindings/tree/master/samples/MobileBlazorBindingsWeather/Microsoft.MobileBlazorBindings.PancakeView). To learn more about how to wrap Xamarin.Forms components for use with Blazor syntax, see [Wrapping Xamarin.Forms components for use with Blazor topic](../advanced/custom-components.md).

1. Dependency injection is used in the weather app with a [`WeatherService` type](https://github.com/xamarin/MobileBlazorBindings/blob/master/samples/MobileBlazorBindingsWeather/MobileBlazorBindingsWeather/WeatherService.cs) that is [registered in the host](https://github.com/xamarin/MobileBlazorBindings/blob/master/samples/MobileBlazorBindingsWeather/MobileBlazorBindingsWeather/App.cs#L16) and consumed in the [`WeatherApp.razor` page](https://github.com/xamarin/MobileBlazorBindings/blob/master/samples/MobileBlazorBindingsWeather/MobileBlazorBindingsWeather/WeatherApp.razor#L1).

   * To learn more, read the [dependency injection topic](../advanced/dependency-injection.md).

1. Component initialization enables running initialization code when a component is run. The weather app uses this to load the initial weather data when the app starts by overriding the [`OnInitialized` method](https://github.com/xamarin/MobileBlazorBindings/blob/master/samples/MobileBlazorBindingsWeather/MobileBlazorBindingsWeather/WeatherApp.razor#L140-L144):

    ```c#
    protected override void OnInitialized()
    {
        CurrentWeather = WeatherService.GetWeatherReport();
        Temperature = CurrentWeather.Temperature;
    }
    ```

   To learn more, including how to do async initialization, check out the [Blazor lifecycle methods documentation](/aspnet/core/blazor/lifecycle).

1. CSS styles are used to apply common properties by element type or by CSS class name. A [CSS file](https://github.com/xamarin/MobileBlazorBindings/blob/master/samples/MobileBlazorBindingsWeather/MobileBlazorBindingsWeather/WeatherStyles.css) is included as an embedded resource in the shared project (this is the default setting for CSS files). Learn more about using CSS in Mobile Blazor Bindings in the [CSS Styles topic](../ui/css-styles.md).
