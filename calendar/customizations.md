---
title: Customizations
page_title: Calendar Customizations
position: 8
---

# Calendar: Customizations

<img src="../images/calendar-customization001.png"/>

<code>TKCalendar</code> allows customizing almost evety aspect of its visual appearance. This article demonstrates some of the customization techniques that can be used with it.

<code>TKCalendar</code> comes with two predefined themes:
- <code>TKCalendarDefaultTheme</code> - a default theme
- <code>TKCalendarIPadTheme</code> - a theme designed for iPad

You can switch between themes by usig the <code>theme</code> property:

```Objective-C
TKCalendar *calendar = [[TKCalendar alloc] initWithFrame:self.view.bounds];
calendar.theme = [TKCalendarIPadTheme new];
```
```Swift
let calendar = TKCalendar(frame: self.view.bounds)
calendar.theme = TKCalendarIPadTheme()
```
```C#
TKCalendar calendar = new TKCalendar (this.View.Bounds);
calendar.Theme = new TKCalendarIPadTheme ();
```

<code>TKCalendar</code> uses presenter classes to render different view modes. They all inherit from <code>UIView</code> and contain subviews with settings that can be changed. Most useful settings are grouped in a style property in the presenter class:

```Objective-C
TKCalendarMonthPresenter *presenter = (TKCalendarMonthPresenter*)calendar.presenter;
presenter.style.titleCellHeight = 40;
presenter.style.backgroundColor = [UIColor redColor];
presenter.headerIsSticky = YES;
```
```Swift
let presenter = calendar.presenter() as TKCalendarMonthPresenter
presenter.style().titleCellHeight = 40
presenter.style().backgroundColor = UIColor.redColor()
presenter.headerIsSticky = true
```
```C#
TKCalendarMonthPresenter presenter = (TKCalendarMonthPresenter)calendar.Presenter;
presenter.Style.TitleCellHeight = 40;
presenter.Style.BackgroundColor = UIColor.Red;
presenter.HeaderIsSticky = true;
```

There are cases when specific cells must have custom design based on the cell state (e.g. today, weekend, selected). This can be dobe by adopging the <code>TKCalendarDelegate</code> protocol and implementing its <code>calendar:upateVisualsForCell:</code> method:
```Objective-C
- (void)calendar:(TKCalendar*)calendar updateVisualsForCell:(TKCalendarCell*)cell;
{
    if ([cell isKindOfClass:[TKCalendarDayCell class]]) {
        TKCalendarDayCell *dayCell = (TKCalendarDayCell*)cell;
        if (dayCell.state & TKCalendarDayStateToday) {
            cell.style.textColor = [UIColor colorWithRed:0.0039 green:0.5843 blue:0.5529 alpha:1.0000];
        }
    }
}
```
```Swift
func calendar(calendar: TKCalendar!, updateVisualsForCell cell: TKCalendarCell!) {
    if cell.isKindOfClass(TKCalendarDayCell) {
        let dayCell: TKCalendarDayCell = cell as TKCalendarDayCell
        var a:Int = dayCell.state.toRaw()
        if (dayCell.state.toRaw() & TKCalendarDayState.Today.toRaw()) != 0 {
            cell.style().textColor = UIColor(red: 0.0039, green: 0.5843, blue: 0.5529, alpha: 1.0000)
        }
    }
}
```
```C#
public override void UpdateVisualsForCell (TKCalendar calendar, TKCalendarCell cell)
{
	if (cell is TKCalendarDayCell) {
		TKCalendarDayCell dayCell = (TKCalendarDayCell)cell;
		if ((dayCell.State & TKCalendarDayState.Today) != 0) {
			cell.Style.TextColor = new UIColor (0.0039f, 0.5843f, 0.5529f, 1.0f);
		}
	}
}
```

The cell can be replaced with a custom one for more complex scenarios. This can be done by implementing the <code>calendar:viewForCellOfKind:</code> method of <code>TKCalendarDelegate</code> protocol:
```Objective-C
- (TKCalendarCell *)calendar:(TKCalendar *)calendar viewForCellOfKind:(TKCalendarCellType)cellType
{
   	if (cellType == TKCalendarCellTypeDay) {
       	CustomCell *cell = [CustomCell new];
       	return cell;
   	}
   	return nil;
}
```
```Swift
func calendar(calendar: TKCalendar!, viewForCellOfKind cellType: TKCalendarCellType) -> TKCalendarCell! {
    if cellType == TKCalendarCellType.Day {
        let cell = CustomCell()
        return cell
    }
    return nil
}
```
```C#
public override TKCalendarCell ViewForCellOfKind (TKCalendar calendar, TKCalendarCellType cellType)
{
	if (cellType == TKCalendarCellType.Day) {
		CustomCell cell = new CustomCell ();
		return cell;
	}
	return null;
}
```

The following is the implementation of the <code>CustomCell</code> class:

	@interface CustomCell : TKCalendarDayCell
	@end

	@implementation CustomCell

	- (instancetype)initWithFrame:(CGRect)frame
	{
    	self = [super initWithFrame:frame];
    	if (self) {
    	}
    	return self;
	}

	- (void)updateVisuals
	{
    	[super updateVisuals];

  	    if (self.state & TKCalendarDayStateToday) {
    	    self.label.textColor = [UIColor redColor];
   	    }
   	    else {
   	    	self.label.textColor = [UIColor blueColor];
   	    }
	}

	@end
```Swift
class CustomCell: TKCalendarDayCell {
    override func updateVisuals() {
        super.updateVisuals()
        
        if self.state.toRaw() & TKCalendarDayState.Today.toRaw() != 0 {
            self.label.textColor = UIColor.redColor()
        }
        else {
            self.label.textColor = UIColor.blueColor()
        }
    }
}
```
```C#
public class CustomCell : TKCalendarDayCell
{
	public CustomCell ()
	{
	}

	public override void UpdateVisuals ()
	{
		base.UpdateVisuals ();

		if ((this.State & TKCalendarDayState.Today) != 0) {
			this.Label.TextColor = UIColor.Red;
		} else {
			this.Label.TextColor = UIColor.Blue;
		}
	}
}
```

The result is presented below:

<img src="../images/calendar-customization002.png"/>
