---
title: 'Walkthrough: Build your first app with Experimental Mobile Blazor Bindings'
---

# Build your first app

The easiest way to get started with Experimental Mobile Blazor Bindings is to create the initial project from the command line.

> [!NOTE]
> If you're using nightly dev builds from GitHub, [add a NuGet.config file to point to the nightly feed](../contribute/nightly-builds.md). For official releases, including previews, this step is not needed.

1. Open a command prompt or shell window
1. Install the Experimental Mobile Blazor Bindings project templates by running this command:

    ```shell
    dotnet new -i Microsoft.MobileBlazorBindings.Templates::0.1.129-beta
    ```

    > [!NOTE]
    > If you are using nightly dev builds, specify the template package source by appending this parameter to the command: `--nuget-source https://devdiv.pkgs.visualstudio.com/_packaging/Emblazon/nuget/v3/index.json`)

1. Create projects using the project templates by running this command:

    ```shell
    dotnet new mobileblazorbindings -o FirstMobileBlazorBindingsApp
    ```

    This will create a folder named `FirstMobileBlazorBindingsApp` with the solution file (SLN) and three projects in sub-directories:

   1. `FirstMobileBlazorBindingsApp/FirstMobileBlazorBindingsApp.csproj` - this is the shared project that will contain the UI and logic of your mobile application.
   1. `FirstMobileBlazorBindingsApp.Android/FirstMobileBlazorBindingsApp.Android.csproj` - this is the "backend" project for targeting Android devices. Run this project to launch the app in the Android Emulator.
   1. `FirstMobileBlazorBindingsApp.iOS/FirstMobileBlazorBindingsApp.iOS.csproj` - this is the "backend" project for targeting iOS devices. Run this project to launch the app in the iOS Emulator.

1. You are now ready to open the solution in Visual Studio. The solution in Visual Studio should look like this:

    [ ![Solution Explorer with all 3 projects](media/build-first-app/solution-explorer-with-all-projects-inline.png) ](media/build-first-app/solution-explorer-with-all-projects-expanded.png#lightbox)

1. To run the project, you'll need to set one of the "backend" projects as your startup project. In Solution Explorer, right-click on the Android or iOS project and select `Set as StartUp Project`.

    [ ![Set startup project in Solution Explorer](media/build-first-app/set-startup-project-inline.png) ](media/build-first-app/set-startup-project-expanded.png#lightbox)

1. Press <kbd>F5</kbd> to launch the project in the emulator with the debugger attached (or press <kbd>Ctrl</kbd>+<kbd>F5</kbd> to run without the debugger)

1. Your first application will launch in the emulator and look like this:

    [ ![Hello World running in the Android Emulator](media/build-first-app/android-helloworld-inline.png) ](media/build-first-app/android-helloworld-expanded.png#lightbox)

1. Congratulations, you've created and run your first Experimental Mobile Blazor Bindings app!

To learn more about how this works, go to the [Hello World Walkthrough](hello-world.md).
