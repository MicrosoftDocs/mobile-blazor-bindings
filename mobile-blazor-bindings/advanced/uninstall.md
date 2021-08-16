---
title: 'Uninstall Mobile Blazor Bindings - Mobile Blazor Bindings'
ms.topic: article
ms.prod: aspnet-core
---

# Uninstall Mobile Blazor Bindings

[!INCLUDE [experiment-warning](../includes/experiment-warning.md)]

To uninstall Experimental Mobile Blazor Bindings from your computer, run the following command:

```shell
dotnet new -u Microsoft.MobileBlazorBindings.Templates
```

This will uninstall the project templates from your computer, making them no longer available for use with the `dotnet new` command. Other content from Experimental Mobile Blazor Bindings may be on your computer wherever you already created projects or in various caches.

To verify the templates are uninstalled, run the following command and verify that the `Microsoft.MobileBlazorBindings.Templates` package is gone:

```shell
dotnet new -u
```
