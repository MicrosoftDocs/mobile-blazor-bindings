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

[ ![Hello World running in the Android Emulator](media/index/hello-world.png) ](media/index/hello-world.png#lightbox)

