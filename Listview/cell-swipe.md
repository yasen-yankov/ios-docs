---
title: Cell swipe gesture
page_title: ListView cell swipe gesture
position: 9
---

# ListView: Cell swipe gesture


When enabled this feature allows end users to use swipe gesture on cells. When users swipes the content view will move revealing a designated swipe background view where you can place custom views ready for interaction e.g. buttons images etc.

<screenshot>
## Enabling cell swipe gesture ##
Use the <code>allowsCellSwipe</code> property to allow the user to perform swipe gesture on cells.
<snippets>
## Configuring cell swipe gesture ##
Use the <code>cellSwipeLimits</code>  property to set how far the cell may be swiped.
<snippets>

Use the <code>cellSwipeTreshold</code> property to se the minimum distance the user needs to swipe before the gesture is considered effective. If the user swipes bellow the treshold the cell will auto revert to its original state.
<snippets>


Use the <code>cellSwipeAnimationDuration</code> property to set the cell swipe animation duration 

## Responding to swipe interactions##
In order to respond programatically to a swipe gesture performed by user you will need to implement one or mor of the following methods from the TKListViewDelegate protocol.
- listView:shouldSwipeCell:atIndexPath:
- listView:didSwipeCell:atIndexPath:withOffset:
- listView:didFinishSwipeCell:atIndexPath:withOffset:
- listView:didFinishSwipeCell:atIndexPath:withOffset:

<snippets>