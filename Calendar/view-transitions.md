---
title: Transitions
page_title: Calendar View Transitions
position: 5
---

# Calendar: View Transitions

View transitions allow for switching to the next/previous month with different animation effects. Those effects are available in all view mode presenters that inherit from <code>TKCalendarPresenterBase</code>. These include: month, month names, year numbers. Detailed information about view modes is available in this help article: [View modes](view-mode)

<img src="../images/calendar-view-transitions001.png"/>

The available animations are: *card, flip, flow, fold, rotate, and scroll*. The default transition is *scroll*. You should access the <code>transitionMode</code> property of the presenter class in order to customize the transition effect:

```Objective-C
TKCalendarMonthPresenter *presenter = (TKCalendarMonthPresenter*)calendarView.presenter;
presenter.transitionMode = TKCalendarTransitionModeFold;
```
```Swift
let presenter = calendarView.presenter() as! TKCalendarMonthPresenter
presenter.transitionMode = TKCalendarTransitionModeFold
```
```C#
TKCalendarMonthPresenter presenter = (TKCalendarMonthPresenter)calendarView.Presenter;
presenter.TransitionMode = TKCalendarTransitionMode.Fold;
```

The following options can be applied on transitions:

The <code>transitionIsVertical</code> changes the horizontal/vertical orientation of the transition, this changes also the activation gesture:

```Objective-C
presenter.transitionIsVertical = YES;
```
```Swift
presenter.transitionIsVertical = true
```
```C#
presenter.TransitionIsVertical = true;
```

The <code>transitionIsReverse</code> changes the forward/backward direction of the transition, thus changing its effect.

```Objective-C
presenter.transitionIsReverse = YES;
```
```Swift
presenter.transitionIsReverse = true
```
```C#
presenter.TransitionIsReverse = true;
```

Finally the transition duration can be customized by setting the <code>transitionDuration</code> property:

```Objective-C
presenter.transitionDuration = 2.;
```
```Swift
presenter.transitionDuration = 2.0
```
```C#
presenter.TransitionDuration = 2.0;
```
