---
title: Point Customization
slug: chart-series-point-customization
tags: Chart, iOS
publish: true
ordinal: 7
---

Customization of data point appearance
======================================

##Overview

The TKChartSeries can draw a point in particular shape. You can customize the appearance and shape of this point by accessing and altering the styling properties and palette items for shapePallete.

Note that the approach above is applicable to any series (except TKChartPieSeries, TKChartBarSeries and TKChartColumnSeries). If you want to change the shape of each point, you should use the following code snippet:

series.style.pointShape = [TKShape shapeWithType:TKShapeTypeStar andSize:16];

<img src="../images/chart-series-point001.png"/>

You can specify many predefined shapes by using the following enum:
    - **TKShapeTypeNone** - No shape
    - **TKShapeTypeSquare** - Square shape
    - **TKShapeTypeCircle** - Circle shape
    - **TKShapeTypeTriangleUp** - Triangle pointing up    
    - **TKShapeTypeTriangleDown** - Triangle pointing down
    - **TKShapeTypeDiamond** - Diamond shape
    - **TKShapeTypeRhombus** - Rhombus shape
    - **TKShapeTypePentagon** - Pentagon shape
    - **TKShapeTypeHexagon** - Hexagon shape
    - **TKShapeTypeStar** - Star shape
    - **TKShapeTypeHeart** - Heart shape

In addition, you can change a point background color by using the following lines of code:

    series.style.pointShape = [[TKShape alloc] initWithType:TKShapeTypeCircle andSize:8];
    TKChartPaletteItem *palleteItem = [[TKChartPaletteItem alloc] init];
    palleteItem.fill = [TKSolidFill solidFillWithColor:[UIColor redColor]];
    series.style.shapePalette = [[TKChartPalette alloc] init];

<img src="../images/chart-series-point002.png"/>



