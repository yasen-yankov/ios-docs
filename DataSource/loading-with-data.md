---
title: Consuming Data
page_title: DataSource Consuming Data
position: 3
---

# DataSource: Consuming Data

TKDataSource can consume data comming from various sources. 

<img chart>

The simplest way to load data in TKDataSource is to use an array with numbers or strings:

```Objective-C
```
```Swift
```
```C#
```

It supports also arrays with business objects. In this scenario you can use displayKey and valueKey properties to define how to present the data:

```Objective-C
```
```Swift
```
```C#
```

When using NSDictionary as a data provider for TKDataSource, its items property contains the keys collection of the dictionary and the itemSource property contains the dictionary itself. The following code manipulates the dictionary by applying sorting and filtering methods and then presents the data:

```Objective-C
```
```Swift
```
```C#
```

TKDataSource is handy also when loading data from resources. In this case it can parse a JSON formatted file and present its data:

```Objective-C
```
```Swift
```
```C#
```

Finally, TKDataSource can be used to present data comming from a web service. The following code downloads a JSON formatted data from a web service, groups the items and presents the result in TKChart:

```Objective-C
```
```Swift
```
```C#
```
