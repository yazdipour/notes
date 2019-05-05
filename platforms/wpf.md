# WPF

## Theme and Controls

* https://github.com/MahApps/MahApps.Metro
* http://materialdesigninxaml.net
* https://nugetmusthaves.com/article/top-wpf-libraries

## Tutorial

https://www.wpf-tutorial.com/

## Panels

* StackPanel
* Canvas
* Grid
* WrapPanel

    * set child controls next to the other horizontally (default) or vertically
    * automatically wraps when there's no more room.

```xml
<WrapPanel Orientation="Vertical">
	<Button>Test button 1</Button>
	<Button>Test button 2</Button>
	<Button>Test button 3</Button>
	<Button Width="140" Height="44">Test button 4</Button>
	<Button>Test button 5</Button>
	<Button>Test button 6</Button>
</WrapPanel>
```

![WrapPanel](https://www.wpf-tutorial.com/Images/ArticleImages/1/chapters/panels/wrappanel_vertical_width_and_height.png)

* DockPanel

```xml
<DockPanel LastChildFill="False">
	<Button DockPanel.Dock="Top" Height="50">Top</Button>
	<Button DockPanel.Dock="Bottom" Height="50">Bottom</Button>
	<Button DockPanel.Dock="Left" Width="50">Left</Button>
	<Button DockPanel.Dock="Left" Width="50">Left</Button>
	<Button DockPanel.Dock="Right" Width="50">Right</Button>
	<Button DockPanel.Dock="Right" Width="50">Right</Button>
</DockPanel>
```

![DockPanel](https://www.wpf-tutorial.com/Images/ArticleImages/1/chapters/panels/dockpanel_last_child_fill_disabled.png)

* UniformGrid: Grid, with rows and columns that have the same size

```xml
<UniformGrid Rows="2" Columns="4".
    FlowDirection="RightToLeft"> <!-- FirstColumn="3" -->
    <Label Content="1" Background="AliceBlue"/>
    <Label Content="2" Background="Cornsilk"/>
    <Label Content="3" Background="DarkSalmon"/>
    <Label Content="4" Background="Gainsboro"/>
    <Label Content="5" Background="LightBlue"/>
    <Label Content="6" Background="MediumAquamarine"/>
    <Label Content="7" Background="MistyRose"/>
</UniformGrid>
```

![UniformGrid](https://2000thingswpf.files.wordpress.com/2012/01/469-001.png)

* GridSplitter

```xml
<GridSplitter Grid.Row="1" Height="5" HorizontalAlignment="Stretch" />
```
![GridSplitter](https://www.wpf-tutorial.com/Images/ArticleImages/1/chapters/panels/grid_splitter_horizontal_not_centered.png)

## Window and Navigation

* Window: its a new Window for your application. You should use it when you want to pop up an entirely new window.

* Page is a page inside your Window. It is mostly used for web-based systems like an XBAP, where you have a single browser window and different pages can be hosted in that window.

* Window navigation: `new MyWindow().Show();`

* ***Navigation with Frame - Page***:

```xml
<Window>
    <Frame x:Name="_mainFrame" />
</Window>
```

```csharp
_mainFrame.Navigate(new Page1());
//Using NavigationService
_mainFrame.NavigationService.Navigate(new Page1());
_mainFrame.NavigationService.GoBack();
_mainFrame.NavigationService.GoForward();
_mainFrame.NavigationService.Refresh();
_mainFrame.NavigationService.Navigate(new Uri("http://www.google.com/"));
_mainFrame.NavigationService.Navigate(new Uri("Page1.xaml", UriKind.Relative));
_mainFrame.NavigationService.Navigate(new Button());
_mainFrame.NavigationService.Navigate("Hello world");
```

* Navigate with Hyperlink in Pages:

```xml
<Hyperlink NavigateUri="Page2.xaml?Message=Hello">Go to page 2</Hyperlink>
```

And extract the parameters via `NavigationService.CurrentSource`, which returns a Uri object.

* Navigation with UserControl:

`ContentArea.Content = new MyUserControl();`

```xml
<Window x:Class="MyNamespace.MainWindow" ...>
    <DockPanel>
        <ContentControl x:Name="ContentArea" />
    </DockPanel>
</Window>
```

* MVVM Navigation

https://www.codeproject.com/Articles/72724/Beginning-a-WPF-MVVM-application-Navigating-betwee

## Binding

* Commands

https://www.wpf-tutorial.com/commands/using-commands/

* StringFormat

```xml
<TextBlock Text="{Binding Source={x:Static system:DateTime.Now}, ConverterCulture='ja-JP', StringFormat=Japanese date: {0:D}}" />
```

* Convert

```xml
<CheckBox IsChecked="{Binding ElementName=txtValue, Path=Text, Converter={StaticResource YesNoToBooleanConverter}}" Content="Yes" />
```

```c#
public class YesNoToBooleanConverter : IValueConverter
{
	public object Convert(object value, Type targetType, object parameter, System.Globalization.CultureInfo culture) => true;
	public object ConvertBack(object value, Type targetType, object parameter, System.Globalization.CultureInfo culture) => "yes";
}
```

* INotifyPropertyChanged

```c#
public class User : INotifyPropertyChanged
{
	private string name;
	public string Name {
		get { return this.name; }
		set {
			if(this.name != value)
			{
			    this.name = value;
			    this.NotifyPropertyChanged("Name");
			}
		}
	}

	public event PropertyChangedEventHandler PropertyChanged;

	public void NotifyPropertyChanged(string propName)
	{
		if(this.PropertyChanged != null)
			this.PropertyChanged(this, new PropertyChangedEventArgs(propName));
	}
}
```
