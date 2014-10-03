---
title: Localization
position: 7
---

# Calendar: Localization

<img src="../images/calendar-localization001.png"/>

By defualt, <code>TKCalendar</code> uses the current system locale and calendar settings. However, it allows for specifying those settings explicitly, overriding the system settings. This article describes how to do this.

The <code>calendar</code> property of <code>TKCalendar</code> specifies the <code>NSCalendar</code> to be used. You can use this property to change the first day in week to Monday for example:

```Objective-C
NSCalendar *calendar = [[NSCalendar alloc] initWithCalendarIdentifier:NSGregorianCalendar];
calendar.firstWeekday = 2;
TKCalendar *calendarView = [[TKCalendar alloc] initWithFrame:self.view.bounds];
calendarView.calendar = calendar;
```
```Swift
let calendar = NSCalendar(calendarIdentifier: NSGregorianCalendar)
calendar.firstWeekday = 2
let calendarView = TKCalendar(frame: self.view.bounds)
calendarView.calendar = calendar
```
```C#
NSCalendar calendar = new NSCalendar (NSCalendarType.Gregorian);
calendar.FirstWeekDay = 2;
TKCalendar calendarView = new TKCalendar (this.View.Bounds);
calendarView.Calendar = calendar;
```

<img src="../images/calendar-localization002.png"/>

Or, you can change the calendar with one specific for your users:

```Objective-C
calendarView.calendar = [[NSCalendar alloc] initWithCalendarIdentifier:NSChineseCalendar];
```
```Swift
calendarView.calendar = NSCalendar(calendarIdentifier: NSChineseCalendar)
```
```C#
calendarView.Calendar = new NSCalendar (NSCalendarType.Chinese);
```

Month names and week day names are provided by the <code>locale</code> property. Use the following code to customize the current locale:

```Objective-C
calendarView.locale = [[NSLocale alloc] initWithLocaleIdentifier:@"ru_RU"];
```
```Swift
calendarView.locale = NSLocale(localeIdentifier: "ru_RU")
```
```C#
calendarView.Locale = new NSLocale ("ru_RU");
```

After modifying the locale you should call the <code>update:</code> method for the presenter:

```Objective-C
[calendarView.presenter update:NO];
```
```Swift
calendarView.presenter().update(false)
```
```C#
calendarView.Presenter.Update (false);
```

<img src="../images/calendar-localization003.png"/>


