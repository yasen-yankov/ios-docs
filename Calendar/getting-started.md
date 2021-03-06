---
title: Getting Started
page_title: Calendar Getting Started
position: 2
---

# Calendar: Getting Started

This quick start tutorial demonstrates how to create a simple iOS application with <code>TKCalendar</code>.

<img src="../images/calendar-gettingstarted001.png"/>

## Prerequisites

This article assumes that you have followed the *Downloading UI for iOS*, *Installing UI for iOS* and *Setting Up the project* steps from [the common Getting Started article](../getting-started).

## Setting up TKCalendar

Now that our project is created and the TelerikUI.framework is added, we can start referencing and using the TelerikUI types:

Open your <code>ViewController.m</code> file and add a reference to Telerik UI header file:

    #import <TelerikUI/TelerikUI.h>

Note that starting with Xcode 6 Apple doesn't generate the precompiled headers file automatically. That is why you should add import the UIKit framework before importing TelerikUI:

    #import <UIKit/UIKit.h>
    
If you are writing Swift, add the same line in your bridging header.

Type the following code in <code>viewDidLoad</code> method:

```Objective-C
TKCalendar *calendarView = [[TKCalendar alloc] initWithFrame:self.view.bounds];
calendarView.autoresizingMask = UIViewAutoresizingFlexibleWidth | UIViewAutoresizingFlexibleHeight;
[self.view addSubview:calendarView];
```
```Swift
let calendarView = TKCalendar(frame: self.view.bounds)
calendarView.autoresizingMask = UIViewAutoresizing.FlexibleHeight | UIViewAutoresizing.FlexibleWidth
self.view.addSubview(calendarView)
```
```C#
TKCalendar calendarView = new TKCalendar (this.View.Bounds);
calendarView.AutoresizingMask = UIViewAutoresizing.FlexibleWidth | UIViewAutoresizing.FlexibleHeight;
this.View.AddSubview (calendarView);
```

This code creates a new instance of <code>TKCalendar</code> and adds it as a subview of the ViewController's main view. The <code>autoresizingMask</code> property is set in order to allow correct resizing of the calendar when the device is rotated in landscape mode.

The next step is to create some random data that will be consumed by the calendar. You can use the following code:

```Objective-C
self.events = [NSMutableArray new];
NSCalendar *calendar = [NSCalendar currentCalendar];
NSDate *date = [NSDate date];
for (int i = 0; i<10; i++) {
    TKCalendarEvent *event = [TKCalendarEvent new];
    event.title = @"Sample event";
    NSDateComponents *components = [calendar components:NSCalendarUnitDay|NSCalendarUnitMonth|NSCalendarUnitYear fromDate:date];
    NSInteger random = arc4random()%20;
    components.day += random > 10 ? 20 - random : -random;
    event.startDate = [calendar dateFromComponents:components];
    components.hour += 2;
    event.endDate = [calendar dateFromComponents:components];
    event.eventColor = [UIColor redColor];
    [self.events addObject:event];
}
```
```Swift
var events = NSMutableArray()
var calendar = NSCalendar.currentCalendar()
var date = NSDate()
for i in 0..<10 {
    let event = TKCalendarEvent()
    event.title = "Sample event"
    let components = calendar.components(NSCalendarUnit.DayCalendarUnit | NSCalendarUnit.MonthCalendarUnit | NSCalendarUnit.YearCalendarUnit | NSCalendarUnit.HourCalendarUnit, fromDate: date)
    let random = Int(arc4random() % 20)
    components.day += random > 10 ? 20 - random : -random
    event.startDate = calendar.dateFromComponents(components)
    components.hour += 2
    event.endDate = calendar.dateFromComponents(components)
    event.eventColor = UIColor.redColor()
    self.events.addObject(event)
}
```
```C#
this.Events = new List<TKCalendarEvent> ();
NSCalendar calendar = NSCalendar.CurrentCalendar;
NSDate date = NSDate.Now;
Random r = new Random ();
for (int i = 0; i < 10; i++) {
	TKCalendarEvent ev = new TKCalendarEvent ();
	ev.Title = "Sample event";
	NSDateComponents components = calendar.Components (NSCalendarUnit.Day | NSCalendarUnit.Month | NSCalendarUnit.Year, date);
	int random = r.Next () % 20;
	components.Day += random > 10 ? 20 - random : -random;
	ev.StartDate = calendar.DateFromComponents (components);
	components.Hour += 2;
	ev.EndDate = calendar.DateFromComponents (components);
	ev.EventColor = UIColor.Red;
	this.Events.Add (ev);
}
```

This code will add 10 events with random dates to an array named <code>events</code>. The <code>arc4random</code> method is being used to create the random dates. The code also assigns a title and a color to the events.

Now let's add this random data to the calendar and present it. In order to do this, we should first adopt the <code>TKCalendarDataSource</code> protocol:

```Objective-C
@interface ViewController () <TKCalendarDataSource>
```
```Swift
class ViewController: UIViewController, TKCalendarDataSource
```
```C#
class CalendarDelegate : TKCalendarDelegate
```

And we should implement its <code>calendar:eventsForDate:</code> method:

```Objective-C
- (NSArray *)calendar:(TKCalendar *)calendar eventsForDate:(NSDate *)date
{
    NSDateComponents *components = [self.calendarView.calendar components:NSCalendarUnitYear|NSCalendarUnitMonth|NSCalendarUnitDay fromDate:date];
    components.hour = 23;
    components.minute = 59;
    components.second = 59;
    NSDate *endDate = [self.calendarView.calendar dateFromComponents:components];
    NSPredicate *predicate = [NSPredicate predicateWithFormat:@"(startDate <= %@) AND (endDate >= %@)", endDate, date];
    return [self.events filteredArrayUsingPredicate:predicate];
}
```
```Swift
func calendar(calendar: TKCalendar!, eventsForDate date: NSDate!) -> [AnyObject]! {
    let components = self.calendarView.calendar.components(NSCalendarUnit.YearCalendarUnit | NSCalendarUnit.MonthCalendarUnit | NSCalendarUnit.DayCalendarUnit, fromDate: date)
    components.hour = 23
    components.minute = 59
    components.second = 59
    let endDate = self.calendarView.calendar.dateFromComponents(components)
    let predicate = NSPredicate(format: "(startDate <= %@) AND (endDate >= %@)", endDate!, date)
    return self.events.filteredArrayUsingPredicate(predicate)
}
```
```C#
public override TKCalendarEventProtocol[] EventsForDate (TKCalendar calendar, NSDate date)
{
	NSDateComponents components = calendar.Calendar.Components (NSCalendarUnit.Day | NSCalendarUnit.Month | NSCalendarUnit.Year, date);
	components.Hour = 23;
	components.Minute = 59;
	components.Second = 59;
	NSDate endDate = calendar.Calendar.DateFromComponents (components);
	List<TKCalendarEventProtocol> filteredEvents = new List<TKCalendarEventProtocol> ();
	for (int i = 0; i < this.main.Events.Count; i++) {
		TKCalendarEventProtocol ev = this.main.Events [i];
		if (ev.StartDate.SecondsSinceReferenceDate <= endDate.SecondsSinceReferenceDate && 
			ev.EndDate.SecondsSinceReferenceDate >= date.SecondsSinceReferenceDate) {
			filteredEvents.Add (ev);
		}
	}
	return filteredEvents.ToArray ();
}
```

Here, the predicate is used to filter the events array by date. Do not forget to assign the <code>dataSource</code> property of <code>TKCalendar</code>:

```Objective-C
calendarView.dataSource = self;
```
```Swift
calendarView.dataSource = self
```
```C#
calendarView.DataSource = new CalendarDataSource (this);
```

For information about populating <code>TKCalendar</code> with EventKit events, please refer to the following article: [Populating with data](populating-with-data)

As a next step you may want to tune up the calendar more precisely by specifying minimum and maximum allowed dates. This can be done by setting the <code>minDate</code> and <code>maxDate</code> properties:

```Objective-C  
calendarView.minDate = [TKCalendar dateWithYear:2010 month:1 day:1 withCalendar:nil];
calendarView.maxDate = [TKCalendar dateWithYear:2016 month:12 day:31 withCalendar:nil];
```
```Swift
calendarView.minDate = TKCalendar.dateWithYear(2010, month: 1, day: 1, withCalendar: nil)
calendarView.maxDate = TKCalendar.dateWithYear(2016, month: 12, day: 31, withCalendar: nil)
```
```C#
calendarView.MinDate = TKCalendar.DateWithYear (2010, 1, 1, null);
calendarView.MaxDate = TKCalendar.DateWithYear (2016, 12, 31, null);
```

By default, <code>TKCalendar</code> displays the current date, use the <code>navigateToDate:animated</code> method to display a different date:

```Objective-C
NSDateComponents *components = [NSDateComponents new];
components.year = 2015;
components.month = 5;
components.day = 1;
NSDate *newDate = [self.calendarView.calendar dateFromComponents:components];
[self.calendarView navigateToDate:newDate animated:NO];
```
```Swift
let components = NSDateComponents()
components.year = 2015
components.month = 5
components.day = 1
let newDate = self.calendarView.calendar.dateFromComponents(components)
self.calendarView.navigateToDate(newDate, animated: false)
```
```C#
NSDateComponents newComponents = new NSDateComponents();
newComponents.Year = 2015;
newComponents.Month = 5;
newComponents.Day = 1;
NSDate newDate = this.CalendarView.Calendar.DateFromComponents (newComponents);
this.CalendarView.NavigateToDate (newDate, true);
```

<code>TKCalendar</code> sends different notifications. For example, in order to be notified when a date was selected, override the <code>calendar:didSelectDate:</code> method of <code>TKCalendarDelegate</code> protocol:

```Objective-C
- (void)calendar:(TKCalendar *)calendar didSelectDate:(NSDate *)date
{
    NSLog(@"%@", date);
}
```
```Swift
func calendar(calendar: TKCalendar!, didSelectDate date: NSDate!) {
    NSLog("%@", date)
}
```
```C#
public override void DidSelectDate (TKCalendar calendar, NSDate date)
{
	Console.WriteLine ("{0}", date);
}
```

Note that <code>TKCalendar</code> supports single, multiple and range date selection. Selection modes are described in detail in the article about [Selection](selection).

Along with selection notifications <code>TKCalendar</code> supports navigation and customization notifications by adopting the <code>TKCalendarDelegate</code> protocol. These notifications are described in the articles about: [Navigation](navigation) and [Customizations](customizations).

Here is the full code of this example:

```Objective-C
#import "ViewController.h"
#import <TelerikUI/TelerikUI.h>

@interface ViewController () <TKCalendarDataSource, TKCalendarDelegate>
@property (nonatomic, strong) NSMutableArray *events;
@end

@implementation ViewController

- (void)viewDidLoad
{
    [super viewDidLoad];
    // Do any additional setup after loading the view.

    TKCalendar *calendarView = [[TKCalendar alloc] initWithFrame:self.view.bounds];
    calendarView.autoresizingMask = UIViewAutoresizingFlexibleWidth | UIViewAutoresizingFlexibleHeight;
    calendarView.dataSource = self;
    calendarView.delegate = self;
    calendarView.minDate = [TKCalendar dateWithYear:2010 month:1 day:1 withCalendar:nil];
    calendarView.maxDate = [TKCalendar dateWithYear:2016 month:12 day:31 withCalendar:nil];
    [self.view addSubview:calendarView];
    self.calendarView = calendarView;

    self.events = [NSMutableArray new];
    NSCalendar *calendar = [NSCalendar currentCalendar];
    NSDate *date = [NSDate date];
    for (int i = 0; i<10; i++) {
        TKCalendarEvent *event = [TKCalendarEvent new];
        event.title = @"Sample event";
        NSDateComponents *components = [calendar components:NSCalendarUnitDay|NSCalendarUnitMonth|NSCalendarUnitYear fromDate:date];
        NSInteger random = arc4random()%20;
        components.day += random > 10 ? 20 - random : -random;
        event.startDate = [calendar dateFromComponents:components];
        components.hour += 2;
        event.endDate = [calendar dateFromComponents:components];
        event.eventColor = [UIColor redColor];
        [self.events addObject:event];
    }

    NSDateComponents *components = [NSDateComponents new];
    components.year = 2015;
    components.month = 5;
    components.day = 1;
    NSDate *newDate = [self.calendarView.calendar dateFromComponents:components];
    [self.calendarView navigateToDate:newDate animated:NO];
}

#pragma mark TKCalendarDataSource

- (NSArray *)calendar:(TKCalendar *)calendar eventsForDate:(NSDate *)date
{
    NSDateComponents *components = [self.calendarView.calendar components:NSCalendarUnitYear|NSCalendarUnitMonth|NSCalendarUnitDay fromDate:date];
    components.hour = 23;
    components.minute = 59;
    components.second = 59;
    NSDate *endDate = [self.calendarView.calendar dateFromComponents:components];
    NSPredicate *predicate = [NSPredicate predicateWithFormat:@"(startDate <= %@) AND (endDate >= %@)", endDate, date];
    return [self.events filteredArrayUsingPredicate:predicate];
}

#pragma mark TKCalendarDelegate

- (void)calendar:(TKCalendar *)calendar didSelectDate:(NSDate *)date
{
    NSLog(@"%@", date);
}

@end
```
```Swift
import UIKit

class ViewController: UIViewController, TKCalendarDataSource, TKCalendarDelegate {

    var events = NSMutableArray()
    
    override func viewDidLoad() {
        super.viewDidLoad()
        let calendarView = TKCalendar(frame: self.view.bounds)
        calendarView.autoresizingMask = UIViewAutoresizing.FlexibleHeight | UIViewAutoresizing.FlexibleWidth
        self.view.addSubview(calendarView)
        calendarView.dataSource = self
        calendarView.delegate = self
        calendarView.minDate = TKCalendar.dateWithYear(2010, month: 1, day: 1, withCalendar: nil)
        calendarView.maxDate = TKCalendar.dateWithYear(2016, month: 12, day: 31, withCalendar: nil)
        
        var calendar = NSCalendar.currentCalendar()
        var date = NSDate()
        for i in 0..<10 {
            let event = TKCalendarEvent()
            event.title = "Sample event"
            let components = calendar.components(NSCalendarUnit.DayCalendarUnit | NSCalendarUnit.MonthCalendarUnit | NSCalendarUnit.YearCalendarUnit | NSCalendarUnit.HourCalendarUnit, fromDate: date)
            let random = Int(arc4random() % 20)
            components.day += random > 10 ? 20 - random : -random
            event.startDate = calendar.dateFromComponents(components)
            components.hour += 2
            event.endDate = calendar.dateFromComponents(components)
            event.eventColor = UIColor.redColor()
            self.events.addObject(event)
        }
        
        let components = NSDateComponents()
        components.year = 2015
        components.month = 5
        components.day = 1
        let newDate = calendarView.calendar.dateFromComponents(components)
        calendarView.navigateToDate(newDate, animated: false)
    }
    
    func calendar(calendar: TKCalendar!, eventsForDate date: NSDate!) -> [AnyObject]! {
        let components = calendar.calendar.components(NSCalendarUnit.YearCalendarUnit | NSCalendarUnit.MonthCalendarUnit | NSCalendarUnit.DayCalendarUnit, fromDate: date)
        components.hour = 23
        components.minute = 59
        components.second = 59
        let endDate = calendar.calendar.dateFromComponents(components)
        let predicate = NSPredicate(format: "(startDate <= %@) AND (endDate >= %@)", endDate!, date)
        return self.events.filteredArrayUsingPredicate(predicate)
    }
    
    func calendar(calendar: TKCalendar!, didSelectDate date: NSDate!) {
        NSLog("%@", date)
    }
}
```
```C#
public class CalendarGettingStarted : UIViewController
{
	public TKCalendar CalendarView {
		get;
		set;
	}

	public List<TKCalendarEvent> Events {
		get;
		set;
	}

	public CalendarGettingStarted ()
	{
	}

	public override void ViewDidLoad ()
	{
		base.ViewDidLoad ();

		TKCalendar calendarView = new TKCalendar (this.View.Bounds);
		calendarView.AutoresizingMask = UIViewAutoresizing.FlexibleWidth | UIViewAutoresizing.FlexibleHeight;
		calendarView.DataSource = new CalendarDataSource (this);
		calendarView.Delegate = new CalendarDelegate ();
		calendarView.MinDate = TKCalendar.DateWithYear (2010, 1, 1, null);
		calendarView.MaxDate = TKCalendar.DateWithYear (2016, 12, 31, null);
		this.View.AddSubview (calendarView);
		this.CalendarView = calendarView;

		this.Events = new List<TKCalendarEvent> ();
		NSCalendar calendar = NSCalendar.CurrentCalendar;
		NSDate date = NSDate.Now;
		Random r = new Random ();
		for (int i = 0; i < 10; i++) {
			TKCalendarEvent ev = new TKCalendarEvent ();
			ev.Title = "Sample event";
			NSDateComponents components = calendar.Components (NSCalendarUnit.Day | NSCalendarUnit.Month | NSCalendarUnit.Year, date);
			int random = r.Next () % 20;
			components.Day += random > 10 ? 20 - random : -random;
			ev.StartDate = calendar.DateFromComponents (components);
			components.Hour += 2;
			ev.EndDate = calendar.DateFromComponents (components);
			ev.EventColor = UIColor.Red;
			this.Events.Add (ev);
		}

		NSDateComponents newComponents = new NSDateComponents();
		newComponents.Year = 2015;
		newComponents.Month = 5;
		newComponents.Day = 1;
		NSDate newDate = this.CalendarView.Calendar.DateFromComponents (newComponents);
		this.CalendarView.NavigateToDate (newDate, true);
		calendarView.ViewMode = TKCalendarViewMode.Year;
	}

	class CalendarDataSource : TKCalendarDataSource
	{
		CalendarGettingStarted main;
		public CalendarDataSource(CalendarGettingStarted main)
		{
			this.main = main;
		}

		public override TKCalendarEventProtocol[] EventsForDate (TKCalendar calendar, NSDate date)
		{
			NSDateComponents components = calendar.Calendar.Components (NSCalendarUnit.Day | NSCalendarUnit.Month | NSCalendarUnit.Year, date);
			components.Hour = 23;
			components.Minute = 59;
			components.Second = 59;
			NSDate endDate = calendar.Calendar.DateFromComponents (components);
			List<TKCalendarEventProtocol> filteredEvents = new List<TKCalendarEventProtocol> ();
			for (int i = 0; i < this.main.Events.Count; i++) {
				TKCalendarEventProtocol ev = this.main.Events [i];
				if (ev.StartDate.SecondsSinceReferenceDate <= endDate.SecondsSinceReferenceDate && 
					ev.EndDate.SecondsSinceReferenceDate >= date.SecondsSinceReferenceDate) {
					filteredEvents.Add (ev);
				}
			}

			return filteredEvents.ToArray ();
		}
	}

	class CalendarDelegate : TKCalendarDelegate
	{
		public override void DidSelectDate (TKCalendar calendar, NSDate date)
		{
			Console.WriteLine ("{0}", date);
		}
	}
}
```

You can easily change the way data is presented in chart by changing the view mode property:

```Objective-C
calendarView.viewMode = TKCalendarViewModeYear;
```
```Swift
calendarView.viewMode = TKCalendarViewModeYear
```
```C#
calendarView.ViewMode = TKCalendarViewMode.Year;
```

All view modes are desctibed in the following article:
[View modes](view-modes)

