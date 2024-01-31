---
title: 'Gestures - Mobile Blazor Bindings'
ms.topic: article
ms.service: aspnet-core
---

# Gestures

[!INCLUDE [experiment-warning](../includes/experiment-warning.md)]

## Overview

Gesture recognizers can be used to detect user interaction with views in applications.

Gesture recognizers are attached to a control and specify which gestures to respond to along with an event to handle the response. Gestures such as tap, pinch, pan, and swipe are supported. Gestures can be added to any component that derives from `View` or `GestureElement`. See the [components reference](components-reference.md) for more details.

## Add a gesture to a component

The following sample adds a tap gesture to a `Label` component and updates its text when it is tapped.

```xml
<ContentView>
    <Label Text="@($"I was tapped {count} times")" FontSize="40">
        <TapGestureRecognizer OnTapped="@OnLabelTapped" />
    </Label>
</ContentView>

@code
{
    int count;

    void OnLabelTapped()
    {
        count++;
        StateHasChanged();
    }
}
```

> [!NOTE]
> The event handler code ends with calling `StateHasChanged()` to tell Blazor to re-render the component. Otherwise the count will be incremented and the change will not be shown.

## Supported gestures

The following example shows the syntax of the supported gestures and their respective events:

```xml
<ContentView>
    <StackLayout>

        <Label Text="...">
            <TapGestureRecognizer NumberOfTapsRequired="1" OnTapped="@OnLabelTapped" />
            <PanGestureRecognizer OnPanUpdated="@OnLabelPanned" />
            <SwipeGestureRecognizer Direction="SwipeDirection.Left" OnSwiped="@OnLabelSwiped" />
            <SwipeGestureRecognizer Direction="SwipeDirection.Right" OnSwiped="@OnLabelSwiped" />
            <PinchGestureRecognizer OnPinchUpdated="@OnLabelPinched" />
        </Label>

    </StackLayout>
</ContentView>

@code
{
    void OnLabelTapped()
    {
        // TODO: Response to tap gesture

        StateHasChanged();
    }

    void OnLabelPanned(PanUpdatedEventArgs e)
    {
        // TODO: Response to pan gesture

        // Check e.StatusType, e.TotalX, and e.TotalY

        StateHasChanged();
    }

    void OnLabelSwiped(SwipedEventArgs e)
    {
        // TODO: Response to swipe gesture

        // Check e.Direction

        StateHasChanged();
    }

    void OnLabelPinched(PinchGestureUpdatedEventArgs e)
    {
        // TODO: Response to pinch gesture

        // Check e.Scale, e.ScaleOrigin, and e.Status

        StateHasChanged();
    }
}
```

## More information

See the [Xamarin.Forms gestures documentation](/xamarin/xamarin-forms/app-fundamentals/gestures/) for more information and examples.
