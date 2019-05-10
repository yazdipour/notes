# UWP

* [create-custom-icon-fonts](https://medium.com/@Niels9001/create-custom-icon-fonts-and-use-them-in-your-uwp-app-1c518febbda1)
* [best-practices](https://github.com/futurice/windows-app-development-best-practices)

## Design Time Data

```xml
<ListView>
    <d:ListView.ItemsSource>
        <x:Array Type="{x:Type models:Item}">
            <models:Item Text="Hello"/>
            <models:Item Text="Hello2"/>
        </x:Array>
    </d:ListView.ItemsSource>
    <ListView.ItemsSource>
        <DataTemplate>
            <ViewCell>
                ...
            </ViewCell>
        </DataTemplate>
    </ListView.ItemsSource>
</ListView>
```

## Functions in x:Bind

* `<object property="{x:Bind pathToFunction.FunctionName(functionParameter1, functionParameter2, ...), bindingProperties}" ... />`
* https://docs.microsoft.com/en-us/windows/uwp/data-binding/function-bindings

```xml
<Grid Background="{x:Bind local:ColorEntry.Brushify(Color), Mode=OneWay}"
<!-- OR -->
<TextBlock x:Name="BigTextBlock" FontSize="20"/>
<TextBlock FontSize="{x:Bind local:ColorEntry.Half(BigTextBlock.FontSize)}" />
```

```c#
class ColorEntry
{
    public static SolidColorBrush Brushify(Color c) => new SolidColorBrush(c);
    public static double Half(double value) => value / 2.0;
```

### StringFormat

```xml
<Page xmlns:sys="using:System">
     <CalendarDatePicker Date="{x:Bind sys:DateTime.Parse(TextBlock1.Text)}" />
     <TextBlock Text="{x:Bind sys:String.Format('{0} is now available in {1}', local:MyPage.personName, local:MyPage.location)}" />
</Page>
```