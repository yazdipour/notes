# Xamarin

...

# Xamarin Forms

## A Gray hLine with 15 margin up and down
`<BoxView HeightRequest="1" Margin="15,0,5,0" BackgroundColor="#eeeeee" />`


## Navigation

```csharp
async void Next_Clicked(object sender, System.EventArgs e)
    => await Navigation.PushModalAsync(new TabsPage());
            
            
// App.cs
public App()
{
  InitializeComponent();
  MainPage = new NavigationPage(new TabsPage());
}
```

## Navigation Style

```xaml
<Style TargetType="NavigationPage">
    <Setter Property="BarBackgroundColor" Value="{StaticResource Primary}" />
    <Setter Property="BarTextColor" Value="White" />
</Style>
```

## Platform Specific

```xaml
<Image Source="graph.png" WidthRequest="320">
  <Image.WidthRequest>
    <OnPlatform x:TypeArguments="x:Double">
        <On Platform="iOS" Value="320" />
        <On Platform="Android" Value="300" />
    </OnPlatform>
  </Image.WidthRequest>
</Image>
```
