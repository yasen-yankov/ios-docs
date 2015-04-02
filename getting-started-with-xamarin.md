---
title: Getting Started - Xamarin.iOS
position: .3
---

# UI for Xamarin.iOS: Getting Started


=======
This quick start tutorial demonstrates how to create a simple Xamarin.iOS application using the Telerik Xamarin.iOS wrappers.

<img src="../images/getting-started-xamarin001.png"/>

## Prerequisites

In order to 

The Telerik Xamarin.iOS wrappers require the following to run:

- A Mac running OS X Mountain Lion or above.
- Latest version of XCode and iOS SDK installed from the [https://itunes.apple.com/us/app/xcode/id497799835?mt=12](App Store).

Telerik UI for Xamarin.iOS works with any of the following setups:

- Latest version of Xamarin Studio on a Mac that fits the above specifications.
- Latest version of Visual Studio Professional or higher on Windows 7 or above, paired with a Mac build host that fits the above specifications. This setup requires a Xamarin Business License or [trial](http://developer.xamarin.com/guides/cross-platform/getting_started/beginning_a_xamarin_trial/).

Below you can find how to download and install the Telerik Xamarin.iOS wrappers.

## Downloading the Telerik Xamarin.iOS wrappers

#### Trial version

There is a Trial version only for UI for Xamarin Cross-Platform as it contains all Telerik Xamarin controls (including Xamarin.iOS wrappers) and will give you a better picture on our Xamarin offering as a whole. You can download the Trial of UI for Xamarin Cross-Platform at [http://www.telerik.com/download/xamarin-ui](http://www.telerik.com/download/xamarin-ui).

#### Paid version

If you have already purchased UI for Xamarin.iOS, UI for Xamarin Cross-Platform or DevCraft Ultimate, you can download the wrappers following the steps below:

1. Go to Your Account >> Products & Subscriptions >> UI for Xamarin.iOS / UI for Xamarin Cross-Platform / DevCraft Ultimate. 
<img src="../images/getting-started-xamarin002.png"/>
2. Click the blue button Download installers and Other Resources. 
	- If you have reached the blue button using your UI for Xamarin.iOS / UI for Xamarin Cross-Platform license, go to step 3
	- If you have reached the blue button using your DevCraft Ultimate, go to step 4. 
<img src="../images/getting-started-xamarin003.png"/> 
3. Clicking the blue button will open the list of files available for download. Download the Manual Installation file of UI for Xamarin.iOS / UI for Xamarin Cross-Platform respectively.
<img src="../images/getting-started-xamarin005.png"/>
4. Clicking the blue button will open the list of products available with the DevCraft Ultimate license. Find the UI for Xamarin Cross-Platform product and click the Download button. This will download the Manual Installation file.
<img src="../images/getting-started-xamarin004.png"/>

## Unpackaging the Telerik Xamarin.iOS wrappers

#### UI for Xamarin Cross-Platform

The UI for Xamarin Cross-Platform products gives you access to a zip file that contains the Xamarin.iOS wrappers, Xamarin.Android wrappers, UI for Windows Phone, Xamarin.Forms controls and a Demo app for these Xamarin.Forms controls. Extract the contents of the zip file to a convenient place, preferably in *C:\Program Files\Telerik\UI for Xamarin\* if you are on Windows or in *Documents\Telerik\UI for Xamarin\* if you are on Mac. After you extract the contents, you can find the Xamarin.iOS assembly at Binaries\iOS\Telerik.Xamarin.iOS.dll

#### UI for Xamarin.iOS

The UI for Xamarin.iOS products gives you access to a zip file that contains the Xamarin.iOS wrappers and a Demo app for these wrappers. Extract the contents of the zip file to a convenient place, preferably in *C:\Program Files\Telerik\UI for Xamarin\* if you are on Windows or in *Documents\Telerik\UI for Xamarin\* if you are on Mac. The Telerik.Xamarin.iOS.dll assembly that contains the Xamarin.iOS wrappers is directly available at the top level  directory of the zip contents. 

## Setting up the project

After downloading and unpackaging the Telerik Xamarin.iOS wrappers, you can proceed with the steps below. As you can develop Xamarin.iOS application with both Visual Studio / Xamarin Studio (again, a license for the Xamarin Platform is required), we will split the tutorial in two parts - one dedicated to Xamarin Studio and one dedicated to Visual Studio

#### Visual Studio

Xamarin Platform offers a Visual Studio plugin that you can use to build Xamarin.iOS applications 

Open Visual Studio / Xamarin Studio and create a new project:

For Visual Studio:
	File >> New Project, then Templates >> Visual C# >> iOS >> iPhone >> Single View App (iOS)

<img src="../images/getting-started-xamarin006.png"/>

For Xamarin Studio:
	File >> New >> Solution, then C# >> Unified API >> iPhone >> Single View Application

<img src="../images/getting-started-xamarin007.png"/>

Add a reference to the Telerik.Xamarin.iOS assembly:

<img src="../images/getting-started-xamarin008.png"/>

Open the RootViewController.cs file from the Solution tree and add the following using directives at the top of the file:


	using TelerikUI;
	using CoreGraphics;
	using System.Collections.Generic;

Thanks to including TelerikUI we have access to the TKChart type. CoreGrapgics provides access to the CGRect type for specifying the rectangle in which the Chart will be rendered, and System.Collections.Generic provides access to the generic List collection.  



In the viewDidLoad method of the RootViewController, type of following code:

```C#
var chart = new TKChart(CGRect.Inflate(this.View.Bounds, -15, -15));
chart.AutoresizingMask = UIViewAutoresizing.FlexibleWidth | UIViewAutoresizing.FlexibleHeight;
this.View.AddSubview(chart);
```

This code creates a new instance of TKChart and adds it as a subview of the RootViewController's main view. The <code>autoresizingMask</code> property is set in order to allow correct resizing of the chart when the device is rotated in landscape mode.

The next step is to create some random data that will be consumed by the chart. You can use the following code:

```C#
Random r = new Random();
var randomNumericData = new List<TKChartDataPoint>();
for (int i = 0; i < 10; i++)
{
    randomNumericData.Add(new TKChartDataPoint(new NSNumber(i), new NSNumber(r.Next(100))));
}

var randomNumericData2 = new List<TKChartDataPoint>();
for (int i = 0; i < 10; i++)
{
    randomNumericData2.Add(new TKChartDataPoint(new NSNumber(i), new NSNumber(r.Next(100))));
}
```

In this case create two lists setting the i variable as an x value, and a random number in the range between 0 and 100 as an y value.

Now let's add this random data to the chart and present it. This is done by the following code:

```C#
chart.AddSeries(new TKChartLineSeries(randomNumericData.ToArray()));
chart.AddSeries(new TKChartLineSeries(randomNumericData2.ToArray()));
```

For more information about populating TKChart with data, please refer to the following article:

[Populating with Data](http://docs.telerik.com/devtools/ios/Chart/populating-with-data)
The TKChartLineSeries tell the chart to present its data in the form of line charts and initialize it with the already created points.

Let's add a title and a legend to our chart. We can do so by setting the corresponding properties to <code>false</code>:

```C#
chart.Title.Hidden = false;
chart.Title.Text = "This is a chart demo";
chart.Legend.Hidden = false;
```

Finally, we can easily employ the built-in animations support to create some fancy animations. To do so, we should set the <code>allowAnimations</code> property to <code>true</code>:

```C#
chart.AllowAnimations = true;
```

For more information about customizing animations, please refer to the following articles:

[Custom Animations](http://docs.telerik.com/devtools/ios/Chart/animations/custom)
[Custom UIKit Dynamics Animations](http://docs.telerik.com/devtools/ios/Chart/animations/custom-uikit-dynamics)

Here is the full code of this example:

```C#
public override void ViewDidLoad()
{
    base.ViewDidLoad();

    var chart = new TKChart(CGRect.Inflate(this.View.Bounds, -15, -15));
    chart.AutoresizingMask = UIViewAutoresizing.FlexibleWidth | UIViewAutoresizing.FlexibleHeight;
    this.View.AddSubview(chart);

    Random r = new Random();
    var randomNumericData = new List<TKChartDataPoint>();
    for (int i = 0; i < 10; i++)
    {
        randomNumericData.Add(new TKChartDataPoint(new NSNumber(i), new NSNumber(r.Next(100))));
    }

    var randomNumericData2 = new List<TKChartDataPoint>();
    for (int i = 0; i < 10; i++)
    {
        randomNumericData2.Add(new TKChartDataPoint(new NSNumber(i), new NSNumber(r.Next(100))));
    }

    chart.AddSeries(new TKChartLineSeries(randomNumericData.ToArray()));
    chart.AddSeries(new TKChartLineSeries(randomNumericData2.ToArray()));

    chart.Title.Hidden = false;
    chart.Title.Text = "This is a chart demo";
    chart.Legend.Hidden = false;

    chart.AllowAnimations = true;
}
```

You can easily change the way data is presented in the Chart by changing the series type:

chart.AddSeries(new TKChartSplineAreaSeries(randomNumericData.ToArray()));
chart.AddSeries(new TKChartSplineAreaSeries(randomNumericData2.ToArray()));

<img src="../images/getting-started-xamarin009.png"/>