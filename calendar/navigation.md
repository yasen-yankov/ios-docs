---
title: Navigation
page_title: Calendar Navigation
position: 6
---

# Calendar: Navigation

This document describes the options to navigate between dates in <code>TKCalendar</code> and the related notifications.

There are two methods in <code>TKCalendar</code> used to navigate forward/backward in the calendar: <code>navigateForward:</code> and <code>navigateBackward:</code>. These methods are context sensitive and the navigation period is specific to the current view mode (e.g. when using a week view the navigation period will be set to one week):

	[calendarView navigateForward:NO];

The calendar will not allow navigating to a date outside of the allowed period, specified by the <code>minDate</code> and <code>maxDate</code> properties:

	calendarView.minDate = minDate;
	calendarView.maxDate = maxDate;

The <code>navigateToDate:animated:</code> method is used to navigate to specific date within the allowed period:

	[calendarView navigateToDate:[NSDate date] animated:YES];

You can determine whether a navigation occurred by implementing <code>TKCalendarDelegate</code> protocol:

	- (void)calendar:(TKCalendar*)calendar didNavigateToDate:(NSDate*)date;
	{
		// Here you can perform the desired action when navigation occured
	}

You should implement the <code>calendar:willNavigateToDate:</code> method if you want to be notified before this action occurs:

	- (void)calendar:(TKCalendar *)calendar willNavigateToDate:(NSDate *)date
	{
    	// Here you can perform the desired action when navigation occured
	}
