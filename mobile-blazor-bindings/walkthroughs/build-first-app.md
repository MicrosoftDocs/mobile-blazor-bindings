---
title: 'Walkthrough: Build your first app with Mobile Blazor Bindings - Mobile Blazor Bindings'
---

# Build your first app

[!INCLUDE [experiment-warning](../includes/experiment-warning.md)]

The easiest way to get started with Experimental Mobile Blazor Bindings is to install and create the initial project from the command line.

> [!NOTE]
> If you have not yet done so, check the [pre-requisites and template installation instructions](../get-started.md).

1. Open a command prompt or shell window

1. Create your project by running this command:

    ```shell
    dotnet new mobileblazorbindings -o FirstMobileBlazorBindingsApp
    ```

    This will create a folder named `FirstMobileBlazorBindingsApp` with the solution file (SLN) and three projects in sub-directories:

   1. `FirstMobileBlazorBindingsApp/FirstMobileBlazorBindingsApp.csproj` - this is the shared project that will contain the UI and logic of your mobile application.
   1. `FirstMobileBlazorBindingsApp.Android/FirstMobileBlazorBindingsApp.Android.csproj` - this is the "backend" project for targeting Android devices. On Windows or Mac you can run this project to launch the app in the Android Emulator.
   1. `FirstMobileBlazorBindingsApp.iOS/FirstMobileBlazorBindingsApp.iOS.csproj` - this is the "backend" project for targeting iOS devices. On Mac you can run this project to launch the app in the iOS Simulator. On Windows you can run it as well if you have a [Mac that is paired](https://docs.microsoft.com/xamarin/ios/get-started/installation/windows/connecting-to-mac/).

1. You are now ready to open the solution in Visual Studio. To open the solution you can double-click the SLN file on your disk, or you can first open Visual Studio 2019, select `File` / `Open` / `Project/Solution`, and then navigate to the new folder you created and select `FirstMobileBlazorBindingsApp.sln`. The solution in Visual Studio should look like this:

    [ ![Solution Explorer with all 3 projects](./media/build-first-app/solution-explorer-with-all-projects-inline.png) ](./media/build-first-app/solution-explorer-with-all-projects-expanded.png#lightbox)

1. To run the project, you'll need to set one of the "backend" projects as your startup project. In Solution Explorer, right-click on the Android or iOS project and select `Set as StartUp Project`.

    [ ![Set startup project in Solution Explorer[(./media/build-first-app/set-startup-project-inline.png) [(./media/build-first-app/set-startup-project-expanded.png#lightbox)

1. Press <kbd>F5</kbd> to launch the project in the emulator with the debugger attached (or press <kbd>Ctrl</kbd>+<kbd>F5</kbd> to run without the debugger)

   * Tip: If you want to run the iOS project on the iOS Simulator, ensure that you select the `iPhoneSimulator` target from the Visual Studio toolbar instead of `iPhone`.

1. Your first application will launch in an emulator or on a device and look like this:

    [ ![Hello World running in the Android Emulator[(./media/build-first-app/android-helloworld-inline.png) [(./media/build-first-app/android-helloworld-expanded.png#lightbox)

1. Congratulations, you've created and run your first Experimental Mobile Blazor Bindings app!

> [!TIP]
> If you're experiencing a problem, refer to the [troubleshooting guide](../advanced/troubleshooting.md).

> [!TIP]
> See the [advanced template options](../advanced/template-options.md) topic for more options when creating a new project.

## Next steps

* To learn more about how this works, go to the [Hello World Walkthrough](hello-world.md).
* To build your first hybrid app, go to the [Hybrid App Walkthrough](build-first-hybrid-app.md).
