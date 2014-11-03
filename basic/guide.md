#Guide
Guide is responsible for axes look and feel: labels, paddings, color, size and other aesthetic parameters. Here is the structure of the chart and related settings:
![guide](../images/guide.png)

And a live example:

```javascript
var chart = new tauChart.Chart({
    guide: {
        x: {label: {text: 'Cycle Time in days', padding: 35}, padding: 20},
        y: {label: 'Effort in points', padding: 20},
        padding: {b: 70, l: 70, t: 10, r: 10},
        showGridLines: 'xy',
        color: {
            brewer: ['color-red', 'color-green', 'color-blue']
        }
    },
    data: defData,
    type: 'scatterplot',
    x: 'cycleTime',
    y: 'effort',
    color: 'team',
    size: 'count'
});
```
[example jsBin](http://jsbin.com/focowi/1/embed?output&height=500px)

##Axis
x or y describes correspontent axis view. We set axis label to 'Count' and define a padding in pixels.
```javascript
  var guide = {
        x:{
           label: { text: 'Count', padding: 36 }
        }
  }
```

## Ticks

Ticks are small indicators on an axis that shows axis values.

#### tickFormat

*guide* allows to format tick labels using *tickFormat* property. TauCharts uses d3-based formatter. Check available [format specifiers](https://github.com/mbostock/d3/wiki/Formatting#d3_format).

```javascript
  var guide = {
        x:{ tickFormat: 's' }
  }
```

In the example above ticks on *x* axis are formatted using SI-prefix (e.g. "22000" printed as "22k").

#### tickPeriod

When operate with *period* scale, *guide* allows to specify the period size.

```javascript
  var guide = {
        x:{ tickPeriod: 'quarter', tickFormat: 'day' }
        // tickPeriod indicates that every tick is a quarter, while tickFormat sets how tick value will be displayed
        // In this example we will have quarters with first day of the quarter: 01-Jan-2014, 01-Apr-2014, 01-Jul-2014, 01-Oct-2014...
  }
```

```javascript
  var guide = {
        x:{ tickPeriod: 'quarter', tickFormat: 'quarter' }
        // Q4 2013, Q1 2014, Q2 2014, Q3 2014...
  }
```

There is a set of pre-defined periods:
- day
- week (split timeline by sundays)
- month
- quarter
- year

Also there is a set of *tickFormat*'s for time-based dimensions:
- "day" (12-Oct-2014)
- "week" (02-Nov-2014) - end date of week
- "week-range" (02-Nov-2014 - 09-Nov-2014) - dates range for the week
- "month" (January 2014, Febrary...) - display month name. January is displayed with a year on the right.
- "month-year" (January 2014, Febrary 2014...)
- "quarter" (Q2 2014)
- "year" (2014)

Also you can [define your own period and tick format](../plugins/customticks.md).

#### tickAutoScale

By default TauChart engine tries to auto scale plot axes for better look and feel by adding some values below and above.

You can avoid this behaviour by setting axis guide property *tickAutoScale* to false:

```javascript
guide: {
    x: { tickAutoScale: false }
}
```

In this case axis values fit to source domain i.e. extreme points will be drawn on the plot borders.

##Coordinate grid

If you want to draw a coordinates grid, you can set *showGridLines*:
```javascript
   var guide = {
        showGridLines:'xy' //show vertical and horizontal line
   }
   //show only x coordinate line
    var guide = {
           showGridLines:'x' //show vertical line
    }
    //or only y
    var guide = {
           showGridLines:'y' //show horizontal line
    }
```

##Color
See [encoding](../advanced/encoding.md#custom-colors-for-encoding-color-value) section to understand how to apply color.
