Let's build a simple scatterplot chart. Download and add tauCharts.js library.

```html
<script type='text/javascript' src='tauCharts.js'>
```
Then [prepare data](../datasource/readme.md) you want to use for the chart. Chart definition is quite straightforward:

```javascript
var chart = new tauChart.Chart({
            data: datasource,
            type: 'scatterplot', // scatterplot, line, bar
            x: 'cycleTime',
            y: 'effort',
            color: 'team',
            size: 'count'
        });
chart.renderTo('#scatter'); // HTML element with 'scatter' id
```

As a result, you will have the chart like that:

[example jsBin](http://jsbin.com/hogoci/16/embed?output)


Currently supported chart types: [scatterplot](scatterplot.md), [line](line.md), [bar](bar.md)

