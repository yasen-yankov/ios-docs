---
title: Populating with Data
page_title: Calendar Populating with Data
position: 3
---

# Calendar: Populating with Data

Following the Model-View-Controller design pattern, the data source mediates between the application's data model (that is, its model objects) and the calendar view. The data source provides the calendar view object with the information it needs to display events.

 <img src="../images/calendar-populating-with-data001.png" />

Following this approach, the <code>TKCalendarDataSource</code> protocol should be implemnted in order to bind <code>TKCalendar</code> with data. This is easy because this protocol contains a single method <code>calendar:eventsForDate:</code>. The adopter should provide the events specific for the provided date. Here is a sample implementation of this method:

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
    let predicate = NSPredicate(format: "(startDate <= %@) AND (endDate >= %@)", endDate, date)
    return self.evets.filteredArrayUsingPredicate(predicate!)
}
```
```C#
public override TKCalendarEvent[] EventsForDate (TKCalendar calendar, NSDate date)
{
	NSDateComponents components = calendar.Calendar.Components (NSCalendarUnit.Year | NSCalendarUnit.Month | NSCalendarUnit.Day, date);
	components.Hour = 23;
	components.Minute = 59;
	components.Second = 59;
	NSDate endDate = calendar.Calendar.DateFromComponents (components);
	List<TKCalendarEvent> filteredEvents = new List<TKCalendarEvent> ();
	for (int i = 0; i < this.main.Events.Count; i++) {
		TKCalendarEvent ev = this.main.Events [i];
		if (ev.StartDate.SecondsSinceReferenceDate <= endDate.SecondsSinceReferenceDate && 
			ev.EndDate.SecondsSinceReferenceDate >= date.SecondsSinceReferenceDate) {
			filteredEvents.Add (ev);
		}
	}

	return filteredEvents.ToArray ();
}
```

In most cases <code>TKCalendar</code> accesses events stored on the device where the application executes. In this scenario the *EventKit* framework should be used. <code>TKCalendar</code> provides a helper data source class which loads the events from device by using the *EventKit API*.

As a prerequisite, the *EventKit* and *EventKitUI* frameworks should be added to the application. Now, you are ready to use the *EventKit* data source helper class for <code>TKCalendar</code>.

The simplest scenario is to create a new instance of <code>TKCalendarEventKitDataSource</code> class and set it as a data source for <code>TKCalendar</code>:

```Objective-C
TKCalendarEventKitDataSource *dataSource = [TKCalendarEventKitDataSource new];

self.calendarView = [[TKCalendar alloc] initWithFrame:self.view.bounds];
self.calendarView.autoresizingMask = UIViewAutoresizingFlexibleWidth | UIViewAutoresizingFlexibleHeight;
self.calendarView.dataSource = dataSource;
[self.view addSubview:self.calendarView];
```
```Swift
let dataSource = TKCalendarEventKitDataSource()

self.calendarView.frame = self.view.bounds
self.calendarView.autoresizingMask = UIViewAutoresizing.FlexibleHeight | UIViewAutoresizing.FlexibleWidth
self.calendarView.dataSource = dataSource
self.view.addSubview(self.calendarView)
```

However, <code>TKCalendarEventKitDataSource</code> supports event filtering. Adopt its <code>TKCalendarEventKitDataSourceDelegate</code> protocol to enable this feature:

```Objective-C
@interface ViewController () <TKCalendarEventKitDataSourceDelegate>
//..
dataSource.delegate = self;
```
```Swift
class ViewController: UIViewController, TKCalendarEventKitDataSourceDelegate
//..
dataSource.delegate = self
```
```C#
//..
dataSource.Delegate = new EventKitDataSourceDelegate ();
```

In order to import only events from calendars local for the device, handle the <code>shouldImportEventsFromCalendar:</code> method:

```Objective-C
- (BOOL)shouldImportEventsFromCalendar:(EKCalendar *)calendar
{
	if (calendar.type == EKCalendarTypeLocal)
    	return YES;
    return NO;
}
```
```Swift
func shouldImportEventsFromCalendar(calendar: EKCalendar!) -> Bool {
    var a = calendar.type
    if calendar.type.value == EKCalendarTypeLocal.value {
        return true
    }
    return false
}
```
```C#
public override bool ShouldImportEventsFromCalendar (MonoTouch.EventKit.EKCalendar calendar)
{
	if (calendar.Type == EKCalendarType.Local) {
		return true;
	}

	return false;
}
```

In the cases when you want to filter only specific events, use the <code>shouldImportEvent:</code> method.
