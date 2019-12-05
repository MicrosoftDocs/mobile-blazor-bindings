---
title: 'Experimental Mobile Blazor Bindings'
---

# Experimental Mobile Blazor Bindings

Experimental Mobile Blazor Bindings is a new framework for building mobile apps using C# and .NET. It brings together familiar web programming patterns for use with native mobile controls to build native mobile apps for Android and iOS. Experimental Mobile Blazor Bindings uses Razor syntax to define UI components and behaviors of an application. The underlying UI components are based on Xamarin.Forms elements.

Blazor runs on [.NET Standard 2.0](https://docs.microsoft.com/dotnet/standard/net-standard) so you can share your .NET code with most other .NET apps.

This is a sample `Hello, World!` component:

```xml
<ContentPage>
    <StackLayout>

        <Label Text="Hello, World!"
               FontSize="20"
               HorizontalTextAlignment="TextAlignment.Center" />

    </StackLayout>
</ContentPage>
```

And here it is running in the Android Emulator:

[ ![Hello World running in the Android Emulator](media/index/hello-world-inline.png) ](media/index/hello-world-expanded.png#lightbox)

To build your first app, check out the [Get Started topic](get-started.md).

And when you're ready for more, check out the walkthroughs:

* [Todo App](walkthroughs/todo-app.md)
* [Weather App](walkthroughs/weather-app.md)

Then some of the advanced topics:

* [Dependency injection](advanced/dependency-injection.md)
* [Wrap Xamarin.Forms components](wrap-xamarin-forms-components.md)

And finally, if you'd like to contribute, check out these topics:

* [Roadmap](contribute/roadmap.md)
* [Feedback](contribute/feedback.md)
