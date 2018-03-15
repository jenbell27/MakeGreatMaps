# Change Over Time

This expression returns the change over time (increase or decrease) by symbols/categories and the actual value of increase or 
decrease by symbol size. For example, if a layer contains two date fields (e.g., 2017 and 2010) the map will show whether each location 
experienced an increase or decrease in value from one time field to the next. The size of the symbol will show how much it increased
or decreased over time. 

## Use cases

Calculating change over time is useful when you have two numeric fields comparing values at two differen times, and you would like to 
indicate the change among the fields. This is common in the visualization profile, 
but it may be used in the popup and labeling profiles as well. This could be used to visualize change in population over time or change in forest area for example.

## Workflow

Copy and paste the expression found in the expression template below to 
the Arcade editor in ArcGIS Online, the relevant location in ArcGIS Pro, or
the relevant location in a custom app.

To configure the script to your layer, you must fill in the two field names that represent each year. Modify the alias
with language that represents change (e.g., gain vs. loss, increase vs. decrease, growth vs. decline, etc.)

For example, in a layer representing forest area by country containing area in 2015 and 1990, you would replace this:

```js
var change = $feature.FIELD_NAME_YEAR1-$feature.FIELD_NAME_YEAR2

When (change > 0, "DESCRIBE INCREASE", change < 0, "DESCRIBE DECREASE", null)
```

With something like the following:

```js
var change = $feature.F2015-$feature.F1990

When (change > 0, "Gain", change < 0, "Loss", null)
```

## Expression Template

```js

// The fields from which to calculate predominance.
// The `value` property must reference a field global variable
// OR an arcade expression that returns a number
// Replace the field names and aliases in ALL CAPS with
// the competing fields in your layer

var fields = [
  { value: $feature.FIELD_NAME_1, alias: "DESCRIBE FIELD_NAME_1 HERE" },
  { value: $feature.FIELD_NAME_2, alias: "DESCRIBE FIELD_NAME_2 HERE" },

  // e.g. { value: $feature.REPUB_VOTES, alias: "Republican Candidate" }
  // ADD MORE FIELDS AS NECESSARY
];

// Returns the predominant category as the alias
// defined in the fields array. If there is a tie,
// then both names are concatenated and used to
// indicate the tie

function getPredominantCategory(fieldsArray){
  var maxValue = -Infinity;
  var maxCategory = "";
  for(var k in fieldsArray){
    if(fieldsArray[k].value > maxValue){
      maxValue = fieldsArray[k].value;
      maxCategory = fieldsArray[k].alias;
    } else if (fieldsArray[k].value == maxValue){
      maxCategory = maxCategory + "/" + fieldsArray[k].alias;
    }
  }
  // totals should exceed zero in predominance visualizations
  return IIF(maxValue <= 0, "none", maxCategory);
}

getPredominantCategory(fields);
```

## Example output

See [this webmap](https://jsapi.maps.arcgis.com/home/webmap/viewer.html?webmap=c453bcc6ab154f8ab7cf7acbeba2ce53) for examples of how to use this expression in ArcGIS Online.

[![predominance](./images/predominance.png)](https://jsapi.maps.arcgis.com/home/webmap/viewer.html?webmap=c453bcc6ab154f8ab7cf7acbeba2ce53)
