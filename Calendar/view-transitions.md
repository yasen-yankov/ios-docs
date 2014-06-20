---
title: Transitions
meta_title: Calendar View Transitions
slug: calendar-view-transitions
tags: calendar, transitions
publish: true
ordinal: 5
---

#Calendar: View Transitions

View transitions allow for switching to the next/previous month with different animation effects. Those effects are available in all view mode presenters that inherit from <code>TKCalendarPresenterBase</code>. These include: month, month names, year numbers. Detailed information about view modes is available in this help article: [View modes](view-mode)

<img src="../images/calendar-view-transitions001.png"/>

The available animations are: *card, flip, flow, fold, rotate, and scroll*. The default transition is *scroll*. You should access the <code>transitionMode</code> property of the presenter class in order to customize the transition effect:

	TKCalendarMonthPresenter *presenter = (TKCalendarMonthPresenter*)calendarView.presenter;
	presenter.transitionMode = TKCalendarTransitionModeFold;

The following options can be applied on transitions:

The <code>transitionIsVertical</code> changes the horizontal/vertical orientation of the transition, this changes also the activation gesture:
	
	presenter.transitionIsVertical = YES;
	
The <code>transitionIsReverse</code> changes the forward/backward direction of the transition, thus changing its effect.

	presenter.transitionIsReverse = YES;
	
Finally the transition duration can be customized by setting the <code>transitionDuration</code> property:

	presenter.transitionDuration = 2.;