---
title: Scroll animations
page_title: ListView Scroll Animations
position: 7
---

# ListView: Scroll Animations

TKListView can animate items on scrolling. It provides several animations effects for items appearing in the viewport while the end-user scrolls - fade-in, slide-in, scale-in. Those can be combined.

<img src="../images/listview-scroll-animations001.png" />

## Adding animation behavior for cells 


In order to add an animation behavior for cells, use the <code>TKListViewCellAppearBehavior</code> property. 

```Objective-C
TKListViewLinearLayout *layout = (TKListViewLinearLayout*)_listView.layout;
layout.itemAppearAnimation = TKListViewItemAnimationFadeIn;
```
```Swift
let layout = listView.layout as! TKListViewLinearLayout
layout.itemAppearAnimation = TKListViewItemAnimation.FadeIn
```
```C#
var layout = this.listView.Layout as TKListViewLinearLayout;
layout.ItemAppearAnimation = TKListViewItemAnimation.FadeIn;
```
