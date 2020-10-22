---
title: 'Advanced template options - Mobile Blazor Bindings'
---

# Advanced template options

[!INCLUDE [experiment-warning](../includes/experiment-warning.md)]

The templates for Mobile Blazor Bindings contain some advanced options to customize the template creation experience.

## Choose which platform projects to create

The project templates have options to skip creation of platform-specific projects if you don't intend to target them. The default is to create all supported platform-specific projects. Use the following options to prevent creation of certain projects.

The Experimental Mobile Blazor Bindings App template supports these options:

```shell
dotnet new mobileblazorbindings --CreateiOSProject false -o AppWithoutiOS
dotnet new mobileblazorbindings --CreateAndroidProject false -o AppWithoutAndroid
```

The Experimental Mobile Blazor Bindings Hybrid App template supports these options:

```shell
dotnet new blazorhybrid --CreateiOSProject false -o AppWithoutiOS
dotnet new blazorhybrid --CreateAndroidProject false -o AppWithoutAndroid
dotnet new blazorhybrid --CreateWindowsProject false -o AppWithoutWindows
dotnet new blazorhybrid --CreatemacOSProject false -o AppWithoutmacOS
```

You can combine multiple options to prevent creation of multiple platform-specific projects:

```shell
dotnet new blazorhybrid --CreateAndroidProject false --CreateiOSProject false -o AppWithoutAndroidAndiOS
```

> [!IMPORTANT]
> The command line options such as `--CreateiOSProject` are _case-sensitive_. An error will be shown if the supplied options don't match supported names.

## Other `dotnet new` options

For a complete reference of `dotnet new` options, refer to the [dotnet new](https://docs.microsoft.com/dotnet/core/tools/dotnet-new) documentation.
