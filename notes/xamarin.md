# Xamarin.Forms

## Shell

* https://nicksnettravels.builttoroam.com/post/2019/04/12/Shell-in-v4-of-XamarinForms-and-Visual-Studio-2019.aspx

## Persian Calender

https://www.dotnettips.info/post/2955/تقویم-شمسی-در-xamarin-forms

## Improve BuildTimes

https://github.com/brminnick/ImproveXamarinBuildTimes

## ConnectionView

https://xamgirl.com/handling-connection-changes-in-xamarin-forms/

## Native Forms

```C#
Xamarin.Forms.Forms.Init();
var settingsView = new SettingsView{BindingContext=settingsViewModel};
var settingsController = settingsView.CreateViewController();
NavigationController.PushViewController(settingsController, true);
```

## XAMLC and Compiled Bindings (x:Bind)

```c#
[assembly:XamlCompilation (XamlCompilationOptions.Compile)]
Namespace MyApp{}
```

```xml
<ListView>
    <ListView.ItemTemplate>
        <DataTemplate x:DataType="{x:Type local:XModel}">
            <Label Text="{Binding Name}">
```

## FastRenderers

```c#
Forms.SetFlags("FastRenderers_Experimetal");
Forms.Init(this,bundle);
```

## LV Fast Scroll

```xml
<ContenxtPage
    xmlns:android="clr-namespace:Xamarin.Forms.PlatformConfiguration.AndroidSpecific;assembly=Xamarin.Forms.Core">
        <ListView android:ListView.IsFastScrollEnabled="true"/>
```

## CollectionView

* Better than ListView
* Uses RecyclerView on Android
* You provide the layout: Grid, Horizontal, Vertical, FlexLayout
* Context Menu
* Gestures

```c#
<CollectionView x:Name="Spaces"/>
Spaces.ItemsLayout = new GridItemsLayout(2, ItemsLayoutOrientation.Vertical);
Spaces.ItemTemplate = new DataTemplate(()=> new SpaceCard());
Spaces.ItemsSource = items;
```

## Platform Specific

```xml
<Image Source="graph.png" WidthRequest="320">
  <Image.WidthRequest>
    <OnPlatform x:TypeArguments="x:Double">
        <On Platform="iOS" Value="320" />
        <On Platform="Android" Value="300" />
    </OnPlatform>
  </Image.WidthRequest>
</Image>
```

or

```xml
<BoxView Margin="{OnPlatform Android=4, iOS=8, Default=10}"/>
```

## Bindable Span (Multiple Labels in One)

```xml
<Label>
    <Label.FormattedText>
        <FormattedString>
            <Span Text="Welcome"/>
            <Span Text="{Binding name}" FontAttributes="Bold"/>
        </FormattedString>
    </Label.FormattedText>
</Label>
```

## Inversion of Control / Dependency Injection

We got IProductsService(interface), ProductsService(impl) and our ViewModel constructor depends on IProductsService.
`public ProductsViewModel(IProductsService productsService){}`

* To access ViewModel Dependecy in View `page.xaml.cs` (The Easy Way)

```c#
BindingContext = ServiceLocator.Current.GetInstance(typeof(ProductsViewModel));
// OR ?NotSure? BindingContext = ServiceLocator.Current.GetInstance<ProductViewModel>();
```

* And we have to link interface and its impl inside DependecyLocator/IoC in `App.xaml.cs` class.

```c#
public App(ITextToSpeech textToSpeech){
    InitializeComponent();
    var unityContainer = new UnityContainer();
    // register dependencies
    unityContainer.RegisterType<IProductsService, ProductsService>();       // Link interface to its impl

    var unityServiceLocator = new UnityServiceLocator(unityContainer);
    ServiceLocator.SetLocatorProvider(() => unityServiceLocator);

    MainPage = new NavigationPage(new ProductsPage());
```

in Unit Test

```c#
  [TestClass]
    public class ProductsUnitTest{
        [TestMethod]
        public void GetProductsTest(){
            // Arrange
            IProductsService productsService = new ProductsService();
            ITextToSpeech mockTextToSpeech = new MockTextToSpeach();
            var vm = new ProductsViewModel(productsService, mockTextToSpeech);
            // Act
            vm.DownloadProducts();
            // Assert
            var expected = productsService.Getproducts();
            var actual = vm.Products;
            Assert.AreEqual(expected, actual);
```

## Dependency_Service

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

## Font

* https://montemagno.com/using-font-icons-in-xamarin-forms-goodbye-images-hello-fonts/
* ANDROID: Copy Fonts inside Android>Assets. Set Build action: AndroidAsset 
* IOS: Copy Fonts inside iOS>Resources and `Fonts provided by application:xx-Medium.ttf`.

```xml
In BundleResource 
<key>UIAppFonts</key>
<array>
  <string>IndieFlower.ttf</string>
</array>
```

* Usage

```xml
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
<!-- OR -->
<Label Text="Welcome to Xamarin.Forms!"
       FontFamily="{StaticResource IndieFlowerFontFamily}"
       FontSize="Large" />
```

## Gesture_Recognizer

```c#
var tapGestureRecognizer = new TapGestureRecognizer();
tapGestureRecognizer.Tapped += (s, e) => {
    // handle the tap
};
image.GestureRecognizers.Add(tapGestureRecognizer);
```

```xml
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

```xml
<Style TargetType="NavigationPage">
    <Setter Property="BarBackgroundColor" Value="{StaticResource Primary}" />
    <Setter Property="BarTextColor" Value="White" />
</Style>
```

## Behaviors

Behaviors are written for a specific control type (or a superclass that can apply to many controls), and they should only be added to a compatible control.

https://docs.microsoft.com/en-us/xamarin/xamarin-forms/app-fundamentals/behaviors/creating

```xml
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

## Drop Shadow/Elevation on Android Bottom Navigation TabbedPage

https://montemagno.com/xamarin-forms-drop-shadow-elevation-on-android-bottom-navigation-tabbedpage/

## Using FontAwesome

https://www.tsjdev-apps.de/fontawesome-in-xamarin-forms-apps/