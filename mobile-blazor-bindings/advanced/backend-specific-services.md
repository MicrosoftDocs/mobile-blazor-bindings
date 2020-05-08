---
title: 'Backend-specific services - Mobile Blazor Bindings'
---

[!INCLUDE [experiment-warning](../includes/experiment-warning.md)]

# Backend-specific services

While many service implementations used in dependency injection have a common implementation for all platforms, there are cases where a platform-specific service implementation needs to be supplied.

Registering backend-specific services involves a few steps:

1. Define a common interface in the shared project. For example, the Todo App sample defines an [`ITextToSpeech` interface](https://github.com/xamarin/MobileBlazorBindings/blob/master/samples/MobileBlazorBindingsTodoSample/MobileBlazorBindingsTodo/ITextToSpeech.cs).

1. Implement the interface in each applicable backend-specific project. It's OK for some backends to not have an implementation. The Todo App sample has an [Android implementation](https://github.com/xamarin/MobileBlazorBindings/blob/master/samples/MobileBlazorBindingsTodoSample/MobileBlazorBindingsTodo.Android/TextToSpeech_Android.cs) and an [iOS implementation](https://github.com/xamarin/MobileBlazorBindings/blob/master/samples/MobileBlazorBindingsTodoSample/MobileBlazorBindingsTodo.iOS/TextToSpeech_iOS.cs).

1. Register the backend-specific implementation in each backend project. In an Android backend, this is done in the [`MainActivity` class `OnCreate` method](https://github.com/xamarin/MobileBlazorBindings/blob/master/samples/MobileBlazorBindingsTodoSample/MobileBlazorBindingsTodo.Android/MainActivity.cs#L26-L30), and in an iOS backend, this is done in the [`AppDelegate` class `FinishedLaunching` method](https://github.com/xamarin/MobileBlazorBindings/blob/master/samples/MobileBlazorBindingsTodoSample/MobileBlazorBindingsTodo.iOS/AppDelegate.cs#L24-L28).

1. In the shared project change the `App` class to take in a constructor parameter `IServiceCollection additionalServices`, as seen [here](https://github.com/xamarin/MobileBlazorBindings/blob/master/samples/MobileBlazorBindingsTodoSample/MobileBlazorBindingsTodo/App.cs#L12).

1. Change the call to `ConfigureServices` to register the backend-specific services with the `AddAdditionalServices` method, as seen [here](https://github.com/xamarin/MobileBlazorBindings/blob/master/samples/MobileBlazorBindingsTodoSample/MobileBlazorBindingsTodo/App.cs#L17-L21).

1. Now you can consume the service as you would consume any other registered service from the dependency injection container. Some examples are shown in the [dependency injection topic](dependency-injection.md). If the service is an optional service because it's not available on all platforms, have the consuming code take in a _list_ of the service, and it will receive either zero instances of the service (if not available) or one instance (if available). An example of this is [here](https://github.com/xamarin/MobileBlazorBindings/blob/master/samples/MobileBlazorBindingsTodoSample/MobileBlazorBindingsTodo/TodoEntryDetails.razor#L2).
