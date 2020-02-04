---
title: 'Xamarin.Essentials'
---

[!INCLUDE [experiment-warning](../includes/experiment-warning.md)]

# Xamarin.Essentials

Xamarin.Essentials provides developers with cross-platform APIs for their mobile applications.

Android, iOS, and UWP offer unique operating system and platform APIs that developers have access to all in C# leveraging Xamarin. Xamarin.Essentials provides a single cross-platform API that works with any Android, iOS, or UWP application that can be accessed from shared code no matter how the user interface is created.

## Get started with Xamarin.Essentials

Follow these steps to access Xamarin.Essentials APIs in your application:

1. Open an existing project, or [create a new project using the templates](../walkthroughs/build-first-app)

1. Add the [**Xamarin.Essentials**](https://www.nuget.org/packages/Xamarin.Essentials/) NuGet package to each project:

    <!--markdownlint-disable MD023 -->
    # [Visual Studio](#tab/windows)

    In the Solution Explorer panel, right click on the solution name and select **Manage NuGet Packages**. Search for **Xamarin.Essentials** and install the package into **ALL** projects including Android, iOS, UWP, and .NET Standard libraries.

    # [Visual Studio for Mac](#tab/macos)

    In the Solution Explorer panel, right click on the project name and select **Add > Add NuGet Packages...**. Search for **Xamarin.Essentials** and install the package into **ALL** projects including Android, iOS, and .NET Standard libraries.

    -----

1. Add a reference to Xamarin.Essentials in any C# class to reference the APIs.

    ```csharp
    using Xamarin.Essentials;
    ```

1. Add a reference to Xamarin.Essentials for Razor files in the `_Imports.razor` file to reference the APIs.

    ```csharp
    @using Xamarin.Essentials
    ```

1. Xamarin.Essentials requires platform-specific setup:

    # [Android](#tab/android)

    Xamarin.Essentials supports a minimum Android version of 4.4, corresponding to API level 19, but the target Android version for compiling must be 9.0, corresponding to API level 28. (In Visual Studio, these two versions are set in the Project Properties dialog for the Android project, in the Android Manifest tab. In Visual Studio for Mac, they're set in the Project Options dialog for the Android project, in the Android Application tab.)

    Xamarin.Essentials installs version 28.0.0.1 of the Xamarin.Android.Support libraries that it requires. Any other Xamarin.Android.Support libraries that your application requires should also be updated to version 28.0.0.1 using the NuGet package manager. All Xamarin.Android.Support libraries used by your application should be the same, and should be at least version 28.0.0.1. Refer to the [troubleshooting page](troubleshooting.md) if you have issues adding the Xamarin.Essentials NuGet or updating NuGets in your solution.

    In the Android project's `MainLauncher` or any `Activity` that is launched Xamarin.Essentials must be initialized in the `OnCreate` method:

    ```csharp
    protected override void OnCreate(Bundle savedInstanceState) {
        //...
        base.OnCreate(savedInstanceState);
        Xamarin.Essentials.Platform.Init(this, savedInstanceState); // add this line to your code, it may also be called: bundle
        //...
    ```

    To handle runtime permissions on Android, Xamarin.Essentials must receive any `OnRequestPermissionsResult`. Add the following code to all `Activity` classes:

    ```csharp
    public override void OnRequestPermissionsResult(int requestCode, string[] permissions, Android.Content.PM.Permission[] grantResults)
    {
        Xamarin.Essentials.Platform.OnRequestPermissionsResult(requestCode, permissions, grantResults);

        base.OnRequestPermissionsResult(requestCode, permissions, grantResults);
    }
    ```

    # [iOS](#tab/ios)

    No additional setup required.

    # [UWP](#tab/uwp)

    No additional setup required.

    -----

1. Follow the [Xamarin.Essentials guides](/xamarin/essentials/) that enable you to copy and paste code snippets for each feature.

## More information

Learn more about Xamarin.Essentials capabilities in the [Xamarin.Essentials documentation](/xamarin/essentials/).
