# Xamarin.Native

...

# Xamarin.Forms

## Font

* Copy Fonts inside iOS>Resources and `Fonts provided by application:xx-Medium.ttf`.
* Copy Fonts inside Android>Assets.

```xaml
<!-- App.xaml -->
    <OnPlatform x:Key="MaterialFontFamily" x:TypeArguments="x:String">
        <On Platform="iOS" Value="Material Design Icons" />
        <On Platform="Android" Value="materialdesignicons-webfont.ttf#Material Design Icons" />
    </OnPlatform>
    <OnPlatform x:Key="MontserratMediumFontFamily" x:TypeArguments="x:String">
        <On Platform="iOS" Value="Montserrat-Medium" />
        <On Platform="Android" Value="Montserrat-Medium.ttf#Montserrat Medium" />
    </OnPlatform>
<!-- Usage -->
    <Setter Property="FontFamily" Value="{StaticResource MaterialFontFamily}" />
```

## Gesture_Recognizer

```c#
var tapGestureRecognizer = new TapGestureRecognizer();
tapGestureRecognizer.Tapped += (s, e) => {
    // handle the tap
};
image.GestureRecognizers.Add(tapGestureRecognizer);
```

```xaml
<Image>
    <Image.GestureRecognizers>
        <TapGestureRecognizer 
            Command="{Binding Source={x:Reference Root}, Path=BindingContext.JobSelectedCommand}"
            CommandParameter="{Binding Id}" NumberOfTapsRequired="1" />
  </Image.GestureRecognizers>
</Image>
```

## Style - Platform Specific

```csharp
//>> in AppDelegate.cs
UWSwitch.Appearance.OnTintColor = UIColor.Red;
UISlider.Appearance.MinimumTrackTintColor = UIColor.Blue;
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

## DependencyService

DependencyService allows apps to call into platform-specific functionality from shared code. 

* 1st Create Interface in SharedProj

```c#
public interface ITextToSpeech {
    void Speak ( string text ); //note that interface members are public by default
```

* 2nd Implement per Platform

```c#
[assembly: Dependency (typeof (TextToSpeech_iOS))]
namespace UsingDependencyService.iOS
{
    public class TextToSpeech_iOS : ITextToSpeech
    {
        public void Speak (string text)
```

* 3rd Use it

```C#
DependencyService.Get<ITextToSpeech>().Speak("Hello");
```

## A Gray hLine with 15 margin up and down
`<BoxView HeightRequest="1" Margin="15,0" BackgroundColor="#eee" />`


## Navigation

```csharp
async void Next_Clicked(object sender, System.EventArgs e)
    => await Navigation.PushModalAsync(new TabsPage());
//
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

## Behaviors

Behaviors are written for a specific control type (or a superclass that can apply to many controls), and they should only be added to a compatible control.

https://docs.microsoft.com/en-us/xamarin/xamarin-forms/app-fundamentals/behaviors/creating

```xaml
<Entry Placeholder="Enter a System.Double">
    <Entry.Behaviors>
        <local:NumericValidationBehavior />
    </Entry.Behaviors>
</Entry>
```

```csharp
public class NumericValidationBehavior : Behavior<Entry>
{
    protected override void OnAttachedTo(Entry entry)
    {
        entry.TextChanged += OnEntryTextChanged;
        base.OnAttachedTo(entry);
    }

    protected override void OnDetachingFrom(Entry entry)
    {
        entry.TextChanged -= OnEntryTextChanged;
        base.OnDetachingFrom(entry);
    }

    void OnEntryTextChanged(object sender, TextChangedEventArgs args)
    {
        double result;
        bool isValid = double.TryParse (args.NewTextValue, out result);
        ((Entry)sender).TextColor = isValid ? Color.Default : Color.Red;
    }
}
```