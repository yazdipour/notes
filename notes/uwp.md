# UWP

https://medium.com/@Niels9001/create-custom-icon-fonts-and-use-them-in-your-uwp-app-1c518febbda1

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