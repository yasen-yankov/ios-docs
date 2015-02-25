---
title: Pull to refresh gesture
page_title: ListView pull to refresh gesture
position: 10
---

# ListView: Pull to refresh

TKListView may be refreshed by a pull-to-refresh gesture. If enabled the feature allows the user to refresh data by swiping his finger down when the content is scrolled up to the top. This will trigger an animated activity indicator which will stay visible until data is refreshed.

<screenshot>


## Allowing pull to refresh##
Use the <code>allowsPullToRefresh</code> property  to enable the feature.
<snippets>

## Responding to the pull to refresh gesture##
To be able to respond to the pull-to-refresh gesture you will need to implement the <code>listViewShouldRefreshOnPull:</code method from the <code>TKListViewDelegate</code>protocol. After fresh data is available you will need notify TKListView by calling the <code>didRefreshOnPull</code> method.Calling this method will allow TKListView to hide the activity indicator and display the fresh data. 

<snippets>





