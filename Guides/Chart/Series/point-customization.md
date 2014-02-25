---
title: Point Customization
meta_title: Point Customization
slug: chart-series-point-customization
tags: Chart, iOS
publish: true
ordinal: 7
---

# Chart Series: Point Customization

The <code>TKChartSeries</code> can draw a point in particular shape. You can customize the appearance and shape of this point by accessing and altering the styling properties and palette items for shapePallete.

Note that the approach above is applicable to any series (except <code>TKChartPieSeries</code>, <code>TKChartBarSeries</code> and <code>TKChartColumnSeries</code>). If you want to change the shape of each point, you should use the following code snippet:

series.style.pointShape = [TKShape shapeWithType:TKShapeTypeStar andSize:16];

<img src="../images/chart-series-point001.png"/>

You can specify many predefined shapes by using the following enum:
    - <code>TKShapeTypeNone</code> - No shape
    - <code>TKShapeTypeSquare</code> - Square shape
    - <code>TKShapeTypeCircle</code> - Circle shape
    - <code>TKShapeTypeTriangleUp</code> - Triangle pointing up    
    - <code>TKShapeTypeTriangleDown</code> - Triangle pointing down
    - <code>TKShapeTypeDiamond</code> - Diamond shape
    - <code>TKShapeTypeRhombus</code> - Rhombus shape
    - <code>TKShapeTypePentagon</code> - Pentagon shape
    - <code>TKShapeTypeHexagon</code> - Hexagon shape
    - <code>TKShapeTypeStar</code> - Star shape
    - <code>TKShapeTypeHeart</code> - Heart shape

In addition, you can change a point background color by using the following lines of code:

    series.style.pointShape = [[TKShape alloc] initWithType:TKShapeTypeCircle andSize:8];
    TKChartPaletteItem *palleteItem = [[TKChartPaletteItem alloc] init];
    palleteItem.fill = [TKSolidFill solidFillWithColor:[UIColor redColor]];
    series.style.shapePalette = [[TKChartPalette alloc] init];

<img src="../images/chart-series-point002.png"/>



