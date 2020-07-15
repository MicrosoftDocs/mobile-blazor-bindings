---
title: 'Dependency Injection - Mobile Blazor Bindings'
---

[!INCLUDE [experiment-warning](../includes/experiment-warning.md)]

# Dependency Injection

Incorporating dependency injection into an application involves a few steps:

   1. Defining an interface of class for the service. The weather app sample foregoes interface definitions due to the simple nature of the app, but would otherwise have an interface named `IWeatherService` with methods on it such as `WeatherReport GetWeatherReport()`.

   1. Implementing the service interface with a concrete implementation. For example:

        ```c#
        public class WeatherService : IWeatherService
        {
            public WeatherReport GetWeatherReport()
            {
                // Get weather report data...
                return weatherReport;
            }
        }
        ```

   1. Registering the service with the host in `App.cs`'s constructor:

        ```c#
        var host = Host.CreateDefaultBuilder()
            .ConfigureServices((hostContext, services) =>
            {
                // Register app-specific services
                services.AddSingleton<IWeatherService, WeatherService>();
            })
            .Build();
        ```

        Several registration methods for services are available on the [`ServiceCollectionServiceExtensions` class](https://docs.microsoft.com/dotnet/api/microsoft.extensions.dependencyinjection.servicecollectionserviceextensions?view=dotnet-plat-ext-3.00).

   1. Consuming the services. There are several ways to consume the services, and two of the most popular ways are:

      1. Constructor injection in custom types also registered in the dependency injection container. To consume a service in this way, add a constructor parameter to your class that uses the service, and when that class is retrieved from the DI container, it will have its parameters populated with other services from the DI container.

      1. Consuming services in `.razor` files is done with the `@inject` directive, which is used in the [`MainPage.razor` file](https://github.com/xamarin/MobileBlazorBindings/blob/master/samples/MobileBlazorBindingsWeather/MobileBlazorBindingsWeather/MainPage.razor#L1):

         ```c#
         @inject WeatherService WeatherService
         ```

         Learn more about the `@inject` directive in the [Blazor documentation](https://docs.microsoft.com/aspnet/core/blazor/dependency-injection?view=aspnetcore-3.0).

> [!TIP]
> In hybrid apps, services are shared between the native UI of the app, the web part of the app, and everywhere else. There are no special steps required to share services and state between areas of hybrid apps.
