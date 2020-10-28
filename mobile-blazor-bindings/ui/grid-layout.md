---
title: 'Grid Layout - Mobile Blazor Bindings'
---

# Grid Layout

[!INCLUDE [experiment-warning](../includes/experiment-warning.md)]

The Grid is a layout that organizes its children into rows and columns, which can have proportional or absolute sizes. By default, a `Grid` contains one row and one column. In addition, a `Grid` can be used as a parent layout that contains other child layouts.

The Grid layout should not be confused with tables, and is not intended to present tabular data. Unlike HTML tables, a `Grid` is intended for laying out content.

To use the Grid you will need to define its _Layout_ of columns and rows, and its _Contents_ to display.

The _layout_ of the grid is defined using `ColumnDefinitions` and `RowDefinitions` to declare the sizes of the columns and rows. The _contents_ of the grid define which controls go in which cells and are wrapped in a `<GridCell>` component to specify the column, row, column span, and row span.

The properties and syntax for defining a grid's layout and contents changed after Preview 4 (version `0.4.74-preview`). Refer to the appropriate section below depending on the version you are using.

## Grid syntax for latest versions (Preview 5 and later)

Starting with Preview 5 the syntax for the Grid component has been simplified:

1. The `<Layout>` and `<Contents>` sections from the `<Grid>` have been removed
1. The row and column definitions are now defined as comma-separated strings instead of as individual collection items
1. The `<GridCell>` components are direct children of the `<Grid>` component

The follow example shows a grid with three rows and two columns:

```xml
<Grid VerticalOptions="LayoutOptions.FillAndExpand" RowDefinitions="Auto, Auto, Auto" ColumnDefinitions="Auto, Auto">
    <GridCell Row="0" Column="0" ColumnSpan="2">
        <Label BackgroundColor="Color.LightBlue" Text="Todo items" FontSize="20" />
    </GridCell>
    <GridCell Row="1" Column="0">
        <Switch IsToggled="true" />
    </GridCell>
    <GridCell Row="1" Column="1">
        <Label Text="Use awesome Xamarin.Forms features" FontSize="20" />
    </GridCell>
    <GridCell Row="2" Column="0">
        <Switch IsToggled="true" />
    </GridCell>
    <GridCell Row="2" Column="1">
        <Label Text="Delight our customers" FontSize="20" />
    </GridCell>
</Grid>
```

## Grid syntax for Preview 4 and earlier

In Preview 4 and earlier the `Grid` component has two child properties:

1. A `Layout` child property where you can define the `ColumnDefinition` and `RowDefinition` elements
1. A `Contents` child property where you can define the contents of the grid's cells

The following example shows a grid with three rows and two columns:

```xml
<Grid VerticalOptions="LayoutOptions.FillAndExpand">
    <Layout>
        <RowDefinition GridUnitType="GridUnitType.Auto" />
        <RowDefinition GridUnitType="GridUnitType.Auto" />
        <RowDefinition GridUnitType="GridUnitType.Auto" />
        <ColumnDefinition GridUnitType="GridUnitType.Auto" />
        <ColumnDefinition GridUnitType="GridUnitType.Auto" />
    </Layout>
    <Contents>
        <GridCell Row="0" Column="0" ColumnSpan="2">
            <Label BackgroundColor="Color.LightBlue" Text="Todo items" FontSize="20" />
        </GridCell>
        <GridCell Row="1" Column="0">
            <Switch IsToggled="true" />
        </GridCell>
        <GridCell Row="1" Column="1">
            <Label Text="Use awesome Xamarin.Forms features" FontSize="20" />
        </GridCell>
        <GridCell Row="2" Column="0">
            <Switch IsToggled="true" />
        </GridCell>
        <GridCell Row="2" Column="1">
            <Label Text="Delight our customers" FontSize="20" />
        </GridCell>
    </Contents>
</Grid>
```

## More information

The Mobile Blazor Bindings Grid component is based on the Xamarin.Forms grid. More information on the Xamarin.Forms grid is available in the [Xamarin.Forms Grid topic](https://docs.microsoft.com/xamarin/xamarin-forms/user-interface/layouts/grid).
