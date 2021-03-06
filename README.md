## Calendar Plugin for Xamarin.Forms
[![Build status](https://dev.azure.com/lilcodelab/Xamarin.Plugin.Calendar/_apis/build/status/Xamarin.Plugin.Calendar-Xamarin.Android-CI)](https://github.com/lilcodelab/Xamarin.Plugin.Calendar) 
[![Nuget](https://img.shields.io/nuget/v/Xamarin.Plugin.Calendar.svg?label=nuget)](https://www.nuget.org/packages/Xamarin.Plugin.Calendar/)
[![Issues](https://img.shields.io/github/issues/lilcodelab/Xamarin.Plugin.Calendar.svg)](https://github.com/lilcodelab/Xamarin.Plugin.Calendar/issues)
[![Chat](https://img.shields.io/badge/Telegram-chat-blue.svg)](https://t.me/XamarinPluginCalendar)
[![License](https://img.shields.io/badge/license-MIT-lightgrey.svg)](https://github.com/lilcodelab/Xamarin.Plugin.Calendar/blob/master/LICENSE)

| Android | iPhone |
| ------- | ------ |
| ![Android Calendar Screenshot](https://github.com/lilcodelab/Xamarin.Plugin.Calendar/blob/master/art/Android.jpg) | ![iPhone Calendar Screenshot](https://github.com/lilcodelab/Xamarin.Plugin.Calendar/blob/master/art/iPhone_XS.png) |

Simple cross platform plugin for Calendar control featuring:
- Displaying events by binding EventCollection
- Localization support with System.Globalization.CultureInfo
- Customizeable colors, fonts and sizes (WIP).

### Setup
* Available on NuGet 
  * https://www.nuget.org/packages/Xamarin.Plugin.Calendar/

#### Supported versions
| Platform | Version |
| -------- | ------- |
| Xamarin.Forms | 3.0+ |
| Xamarin.Android | ? |
| Xamarin.iOS | ? |

### Usage
To get started just install the package via Nuget into your shared and client projects.
You can take a look on the sample app to get started or continue reading.

Reference the following xmlns to your page:
```xml
xmlns:controls="clr-namespace:Xamarin.Plugin.Calendar.Controls;assembly=Xamarin.Plugin.Calendar"
```

Basic control usage:
```xml
<controls:Calendar
        Month="5"
        Year="2019"
        VerticalOptions="FillAndExpand"
        HorizontalOptions="FillAndExpand">
```

Bindable properties:
* `Culture` (CultureInfo)
* `Month` (int)
* `Year` (int)
* `Events` (EventCollection - from package)
* Custom colors, fonts, sizes ...

#### Binding events:
In your XAML, add the data template for events, and bind the events collection, example:
```xml
<controls:Calendar
        Events="{Binding Events}">
    <controls:Calendar.EventTemplate>
        <DataTemplate>
            <StackLayout
                Padding="15,0,0,0">
                <Label
                    Text="{Binding Name}"
                    FontAttributes="Bold"
                    FontSize="Medium" />
                <Label
                    Text="{Binding Description}"
                    FontSize="Small"
                    LineBreakMode="WordWrap" />
            </StackLayout>
        </DataTemplate>
    </controls:Calendar.EventTemplate>
</controls:Calendar>
```

In your ViewModel reference the following namespace:
```csharp
using Xamarin.Plugin.Calendar.Models;
```

Add property for Events:
```csharp
public EventCollection Events { get; private set; }
```

Initialize Events with your data:
```csharp
Events = new EventCollection
{
    [DateTime.Now] = new List<EventModel>
    {
        new EventModel { Name = "Cool event1", Description = "This is Cool event1's description!" },
        new EventModel { Name = "Cool event2", Description = "This is Cool event2's description!" }
    },
    // 5 days from today
    [DateTime.Now.AddDays(5)] = new List<EventModel>
    {
        new EventModel { Name = "Cool event3", Description = "This is Cool event3's description!" },
        new EventModel { Name = "Cool event4", Description = "This is Cool event4's description!" }
    },
    // 3 days ago
    [DateTime.Now.AddDays(-3)] = new List<EventModel>
    {
        new EventModel { Name = "Cool event5", Description = "This is Cool event5's description!" }
    }
},
```

Where `EventModel` is just an example, it can be replaced by any data model you desire.

`EventsCollection` is just a wrapper over `Dictionary<DateTime, ICollection>` exposing custom `Add` method and `this[DateTime]` indexer which internally extracts the `.Date` component of `DateTime` values and uses it as a key in this dictionary.

#### Available color customization
Sample properties:
```xml
MonthLabelColor="Red"
YearLabelColor="Blue"
SelectedDateColor="Red"
SelectedDayBackgroundColor="DarkCyan"
EventIndicatorColor="Red"
EventIndicatorSelectedColor="White"
ArrowsColor="DarkCyan"
DaysTitleColor="Orange"
SelectedDayTextColor="Cyan"
DeselectedDayTextColor="Blue"
OtherMonthDayColor="Gray"
TodayOutlineColor="Blue"
TodayFillColor="Silver"
```

##### TODO
* screenshot of changed colors
* Test Install into your PCL /.NET Standard project and Client projects.
* comment public properties and methods
* More customization, sizes, fonts etc.

Josip Ćaleta @lilcodelab
