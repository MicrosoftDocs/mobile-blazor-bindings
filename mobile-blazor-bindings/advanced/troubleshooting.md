---
title: 'Troubleshooting - Mobile Blazor Bindings'
---

# Troubleshooting Mobile Blazor Bindings

[!INCLUDE [experiment-warning](../includes/experiment-warning.md)]

## Trying to run on iOS, getting "no iOS code signing key" error

If you choose to run the iOS project, you might get an error indicating that there are no iOS code signing keys. That could mean you are trying to deploy to a physical iOS device (such as an iPhone) but without the right configuration. If you intend to use the iOS Simulator, iPhoneSimulator target platform is selected.

[ ![iPhone and iPhoneSimulator target platform selection[(./media/troubleshooting/ios-target-platform-inline.png) [(./media/troubleshooting/ios-target-platform-expanded.png#lightbox)

## Hybrid app doesn't show HTML web UI content

HTML web UI content not showing up could be caused by several reasons. Check each of these in your app:

1. Check for a browser version mismatch. The web UI is shown in a browser component that is hosted inside the native app. The browser component can be dependent on the installed web browsers on the device.

   For WPF (Windows), check that you have [Microsoft Edge Canary Channel](https://www.microsoftedgeinsider.com/download). This version of Microsoft Edge installs side-by-side with other Microsoft Edge installations.

1. Check for script errors in the browser component. Check the [debug hybrid apps](debug-hybrid-apps.md) topic to learn how to check for browser script errors.

1. Check that the platform-specific project calls the appropriate `WebView` `BlazorHybrid` `Init` method (some variations may be expected):

   * Android: In the `MainActivity.cs` file `OnCreate` method call `BlazorHybridAndroid.Init()`:

      ```csharp
        protected override void OnCreate(Bundle savedInstanceState)
        {
            Microsoft.MobileBlazorBindings.WebView.Android.BlazorHybridAndroid.Init();
        ...
          ```

   * iOS: In the `Main.cs` file `Main` method call `BlazorHybridIOS.Init()`:

      ```csharp
        static void Main(string[] args)
        {
            Microsoft.MobileBlazorBindings.WebView.iOS.BlazorHybridIOS.Init();
            ...
      ```

   * Windows: In the `App.cs` file `MainWindow` constructor call `BlazorHybridWindows.Init()`:

      ```csharp
        public MainWindow()
        {
            Microsoft.MobileBlazorBindings.WebView.Windows.BlazorHybridWindows.Init();
            ...
      ```

   * macOS: In the `Main.cs` file `Main` method call `BlazorHybridMacOS.Init()`:

      ```csharp
        private static void Main(string[] args)
        {
            Microsoft.MobileBlazorBindings.WebView.macOS.BlazorHybridMacOS.Init();
            ...
      ```

## CSS styles not working

Refer to the [CSS troubleshooting section](../ui/css-styles.md#troubleshooting).

## Where to go for more solutions

If you're still stuck or have a question, reach out on the [GitHub repo](https://github.com/xamarin/MobileBlazorBindings) by logging an issue.
