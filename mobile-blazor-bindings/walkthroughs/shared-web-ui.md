---
title: 'Walkthrough: Shared Web UI - Mobile Blazor Bindings'
ms.topic: tutorial
ms.service: aspnet-core
---

# Shared Web UI

[!INCLUDE [experiment-warning](../includes/experiment-warning.md)]

Now that you have built a Mobile Blazor Bindings hybrid app that incorporates web UI (HTML with CSS), this walkthrough will show you how to share the web UI with a Blazor Web App so that you can provide your same app UI on the web.

In Blazor this is done by placing the shared UI in a Razor Class Library project, or RCL for short. This enables packaging the web UI and code as a reusable entity that can be referenced by multiple projects in a solution or shared more broadly by distributing it as a NuGet package. An RCL  package can be referenced by a Mobile Blazor Bindings app and a Blazor Web app so that they share the exact same UI.

In this walkthrough you will create a reusable Email Display UI in an RCL and use it in the Mobile Blazor Binding hybrid app and in a Blazor Web app.

> [!NOTE]
> This page is a continuation of the [Build your first hybrid app](build-first-hybrid-app.md) walkthrough. We recommend you complete that walkthrough before continuing.

## Add a Razor Class Library (RCL)

To add an RCL to your app:

1. Right-click on the Solution node in Solution Explorer and select Add / New Project.
1. Locate the Razor Class Library project type and click Next.
1. Enter a name for the project, such as `EmailDisplayUI` and click Create.
1. In the next dialog ensure that following settings are selected: `.NET Core 3.1`, No Authentication, and no support for pages and views, and then click Create.

The new project contains its own Razor files where you will author the web UI and a `wwwroot` folder to contain static assets that are part of this component.

## Add shared web UI to the RCL

1. Right-click on the RCL project and select Add / Class
1. Enter the name `EmailData.cs` and click Add
1. Add a file named `Email.cs` to the RCL
1. Replace its contents with the following C# code:

    ```c#
    namespace EmailDisplayUI
    {
        public class EmailData
        {
            public string From { get; set; }
            public string To { get; set; }
            public string Subject { get; set; }
            public bool IsImportant { get; set; }
            public string Body { get; set; }
        }
    }
    ```

1. Rename `Component1.razor` to `DisplayEmail.razor`
1. Replace its contents with the following Razor markup:

    ```html
    <div class="emailDisplay">
        <div class="emailHeader">
            <div>
                <label>From:</label> @Email.From
            </div>
            <div>
                <label>To:</label> @Email.To
            </div>
            <div>
                <label>Priority:</label> @(Email.IsImportant ? "High" : "Normal")
            </div>
            <div>
                <label>Subject:</label> @Email.Subject
            </div>
        </div>
        <div class="emailBody">
            @Email.Body
        </div>
    </div>

    @code
    {
        [Parameter] public EmailData Email { get; set; }
    }
    ```

1. Change the contents of `wwwroot/styles.css` to the following:

    ```css
    label {
        font-weight: bold;
        font-style: italic;
    }

    .emailDisplay {
        background-image: url('background.png');
    }

    .emailHeader {
        border: 2px solid #808080;
        padding: 1em;
        margin: 1em 0;
    }

    .emailBody {
        border: 1px solid #808080;
        padding: 1em;
        margin: 1em 0;
    }
    ```

## Reference the RCL

To use the RCL you need to reference it from the main UI project so that the UI can be referenced from it. You also need to reference it from the platform-specific projects so that the static assets will be detected and included in those apps.

In each of the FirstBlazorHybridApp, FirstBlazorHybridApp.Android, FirstBlazorHybridApp.iOS, FirstBlazorHybridApp.macOS, and FirstBlazorHybridApp.Windows projects do the following:

1. Right-click on the project and select Add / Project Reference or Add / Reference
1. Select `EmailDisplayUI` and click OK

Now you are ready to use the Email Display UI in your project:

1. In the FirstBlazorHybridApp project open the `WebUI/_Imports_.razor` file and add this line to the end of the file: `@using EmailDisplayUI`
1. In the FirstBlazorHybridApp project open the `WebUI/Pages/Index.razor` file
1. Add the following contents to the bottom of the file:

    ```html
    <DisplayEmail Email="email" />

    @code
    {
        EmailData email = new EmailData { From="sender@example.com", To="recipient@example.com", IsImportant=true, Subject="Learn about Blazor", Body="Tutorials are wonderful!" };
    }
    ```

1. Add a reference to the CSS from each platform-specific project by adding the line `<link href="_content/EmailDisplayUI/styles.css" rel="stylesheet" />` to the `<head>` section:
    * Android: `wwwroot/index.html`
    * iOS: `Resources/wwwroot/index.html`
    * macOS: `Resources/wwwroot/index.html`
    * Windows: `wwwroot/index.html`

## Run the apps to test the UI

You are now ready to test out the new UI! Right-click on any of the Android, iOS, macOS, or Windows projects, select Set as Startup Project, and run the app. You should see the native UI load with the web UI below it, and the web UI should show the email display UI you created.

On the iOS Simulator it should look like this:

[ ![Email display UI running in the iOS Simulator[(./media/shared-web-ui/ios-shared-ui-inline.png) [(./media/shared-web-ui/ios-shared-ui-expanded.png#lightbox)

## Add a Blazor Web project

Now you are ready to re-use the UI you built in a web app!

1. Right-click on the solution node in Solution Explorer and select Add / New Project
1. Select the Blazor App template and click Next
1. Enter a name, such as `FirstBlazorWebApp` and click Create
1. Select the Blazor Server App option, `.NET Core 3.1`, No Auth, Yes for HTTPS, and No for Docker, and click Create.
1. Right-click on the FirstBlazorWebApp project and select Add / Project Reference
1. Select the `EmailDisplayUI` project and click OK
1. Open the `Pages/_Host.cshtml` file and add the line `<link href="_content/EmailDisplayUI/styles.css" rel="stylesheet" />` to the `<head>` section
1. Open the `_Imports.razor` file and add this line to the end of the file: `@using EmailDisplayUI`
1. Open the `Pages/Index.razor` file and add the following contents to the bottom of the file:

    ```html
    <DisplayEmail Email="email" />

    @code
    {
        EmailData email = new EmailData { From="sender@example.com", To="recipient@example.com", IsImportant=true, Subject="Learn about Blazor", Body="Tutorials are wonderful!" };
    }
    ```

1. To run the project, right-click on the project, select Set as Startup Project, and run it. This will start the ASP.NET Core web app and open your default web browser to the app.

It should look like this in your web browser:

[ ![Email display UI running in the web browser[(./media/shared-web-ui/web-shared-ui-inline.png) [(./media/shared-web-ui/web-shared-ui-expanded.png#lightbox)

## Additional resources

To learn more about Razor Class Libraries check out these resources:

* [ASP.NET Core Razor components class libraries](/aspnet/core/blazor/components/class-libraries)
* [Create reusable UI using the Razor class library project in ASP.NET Core](/aspnet/core/razor-pages/ui-class)

## Summary

In this walkthrough you created a Blazor Hybrid app that uses a Razor Class Library (RCL) for a portion of its UI (the email display). You then used that same RCL to host the UI in an ASP.NET Core web application.

This walkthrough showed an example of a read-only UI, but the same techniques can be used to create arbitrarily complex UI with arbitrarily complex application logic to meet any application requirement. You can use patterns such as dependency injection (DI) to create platform-specific services.
