# Unit Conversion

This expression converts one unit of measurement to another. For example, if a layer contains a measurement field in meters, we can use Arcade expressions to convert the value to feet.

## Use cases

Converting units is useful when you have one numeric field that you'd like to represent with another unit of measurement. This is common in the visualization profile as well as the popup and labels profile. This could be used to visualize the depth of the ocean at different contours in meters or in feet. 

## Workflow

Copy and paste the expression found in the expression template below to 
the Arcade editor in ArcGIS Online, the relevant location in ArcGIS Pro, or
the relevant location in a custom app.

To configure the script to your layer, you must fill in the field name that represents the measurement in one unit. 

For example, in a layer representing the depth in meters of ocean contours, you would replace this:

```js
$feature.Field_Name_Meters*3.28
```

With something like the following:

```js
$feature.DepthInMeters*3.28
```
To convert meters to feet, multiply meters by 3.28.

## Expression Template
The first attribute classifies each geometry as either an increase or decrease. This is symbolized by color and/or symbols. 

```js
\\Multiply meters by 3.28 to convert to feet.
$feature.DepthInMeters*3.28
```

## Example output

See [this webmap](http://urbanobservatory.maps.arcgis.com/home/webmap/viewer.html?webmap=6211aae5a03148c4b646376e21afef76) for examples of how to use this expression in ArcGIS Online. 

![Change Over Time](https://i.imgur.com/59i8SbD.png)
