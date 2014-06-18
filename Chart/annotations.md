---
title: Annotations
slug: chart-annotations
tags: Chart, Annotations
publish: true
ordinal: 9
---

# Chart: Annotations

Annotations are visual elements that can be used to highlight certain areas on the plot area and denote statistical significance.

TKChart provides the following types of annotations: 

- <code>TKChartGridLineAnnotation</code>
- <code>TKChartBandAnnotation</code>
- <code>TKChartCrossLineAnnotation</code>
- <code>TKChartBalloonAnnotation</code>
- <code>TKChartLayerAnnotation</code>
- <code>TKChartViewAnnotation</code>

##Adding annotations to the chart##

<code>TKChart</code> contains an <code>annotations</code> collection and annotations can be added to the chart by calling the <code>addAnnotation</code> method. The following code adds a horizontal grid line annotation in TKChart. The annotation requires an axis and a value in order to be initialized correctly.

    [chart addAnnotation:[[TKChartGridLineAnnotation alloc] initWithValue:@80 forAxis:yAxis]];

The annotation visibility can be controlled by setting its <code>hidden</code> property. 
The annotation visual appearance can be changed by using its <code>style</code> property.

##Annotation types##

Conceptually, there are three types of annotations - grid line, band and point annotations. Below is a comparison for each one depending on the scenario.

###Grid line###

The grid line annotation represents a vertical or horizontal line which crosses the entire plot area. It is specified by using the <code>TKChartGridLineAnnotation</code>. 

The line color can be customized by using the annotation initializer:

	TKStroke *stroke = [TKStroke strokeWithColor:[UIColor redColor] width:0.5];
    [_chart addAnnotation:[[TKChartGridLineAnnotation alloc] initWithValue:@80
                                                                   forAxis:_chart.yAxis
                                                                withStroke:stroke]];

<img src="../images/chart-annotations001.png"/>

###Plot band###

The <code>TKChartBandAnnotation</code> is either horizontal or vertical strip, crossing its corresponding axis, specified by its <code>range</code> property. 

    TKRange *range = [[TKRange alloc] initWithMinimum:@10 andMaximum:@40];
    UIColor *color = [UIColor colorWithRed:1. green:0. blue:0. alpha:0.4];
    TKFill *fill = [TKSolidFill solidFillWithColor:color];
    [_chart addAnnotation:[[TKChartBandAnnotation alloc] initWithRange:range
                                                               forAxis:_chart.yAxis
                                                              withFill:fill
                                                            withStroke:nil]];

<img src="../images/chart-annotations002.png"/>

###Point annotations###

Point annotations render their content starting at specific position. Besides the position, a pixel based offset could be added to the point annotation by specifying the <code>offset</code> property.

###Cross line annotation###

The TKChartCrossLineAnnotation is a point annotation which represents two crossing lines with a point at the crossing position.

    [_chart addAnnotation:[[TKChartCrossLineAnnotation alloc] initWithX:@900 Y:@60
                                                              forSeries:_chart.series[0]]];
    
<img src="../images/chart-annotations003.png"/>

###Balloon annotation###

The <code>TKChartBalloonAnnotation</code> displays a balloon-like shape next to the position specified by its arguments. The <code>verticalAlign</code> and <code>horizontalAlign</code> properties allow to position the annotation precisely. The balloon will correct its position automatically if there is not enough space at the specified coordinates.

The following example demonstrates different balloon positions based on the horizontal and vertical alignment:

    TKChartBalloonAnnotation *balloon = [[TKChartBalloonAnnotation alloc] initWithX:@"Mar" Y:@55
                                                                          forSeries:series];
    balloon.text = @"left aligned";
    balloon.style.horizontalAlign = TKChartBalloonHorizontalAlignmentLeft;
    balloon.style.verticalAlign = TKChartBalloonVerticalAlignmentCenter;
    [_chart addAnnotation:balloon];
    
    balloon = [[TKChartBalloonAnnotation alloc] initWithText:@"bottom aligned" X:@"Apr" Y:@30
                                                   forSeries:series];
    balloon.style.verticalAlign = TKChartBalloonVerticalAlignmentBottom;
    [_chart addAnnotation:balloon];

<img src="../images/chart-annotations004.png"/>
 
The <code>attributedText</code> property can be used to present formatted text with NSAttributedString. The following code demonstrates this:

    NSMutableParagraphStyle *paragraphStyle = [[NSParagraphStyle defaultParagraphStyle] mutableCopy];
    paragraphStyle.alignment = NSTextAlignmentCenter;
    NSMutableAttributedString *attributedText = [[NSMutableAttributedString alloc] 
          initWithString:@"Important milestone:\n $55000"
              attributes:@{ NSForegroundColorAttributeName:[UIColor whiteColor],
                            NSParagraphStyleAttributeName:paragraphStyle }];
    [attributedText addAttribute:NSForegroundColorAttributeName value:[UIColor yellowColor] range:NSMakeRange(22, 6)];
    
    TKChartBalloonAnnotation *balloon = [[TKChartBalloonAnnotation alloc] initWithX:@"Mar" Y:@55 forSeries:series];
    balloon.attributedText = attributedText;
    [_chart addAnnotation:balloon];


Almost every aspect of the balloon can be controlled by accessing the <code>style</code> property of the annotation. For example, the <code>arrowSize</code> and the <code>cornerRadius</code>:

    balloon.style.arrowSize = CGSizeMake(20, 20);
    balloon.style.cornerRadius = 0;
	balloon.style.fill = [[TKLinearGradientFill alloc] initWithColors:@[[UIColor grayColor], [UIColor blueColor]]];
	    
<img src="../images/chart-annotations005.png"/>
	
###Layer and view annotations###
	
The <code>TKChartLayerAnnotation</code> and <code>TKChartViewAnnotations</code> are also point annotations. Those allow positioning a layer or a view inside the chart. The following code will position an image named *img* at the center of the chart:

	UIImage *image = [UIImage imageNamed:@"logo"];
    UIImageView *imageView = [[UIImageView alloc] initWithImage:image];
    imageView.bounds = CGRectMake(0, 0, image.size.width, image.size.height);
    imageView.alpha = 0.7;
    [_chart addAnnotation:[[TKChartViewAnnotation alloc] initWithView:imageView X:@550 Y:@90 forSeries:_chart.series[0]]];
	
<img src="../images/chart-annotations006.png"/>
	