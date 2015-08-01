Let's build a simple scatterplot chart. Download and add tauCharts.js library.

```html
<script type='text/javascript' src='tauCharts.js'>
```
Then [prepare data](../datasource/readme.md) you want to use for the chart. The chart definition is quite straightforward:

```javascript
var chart = new tauCharts.Chart({
            data: datasource,
            type: 'scatterplot', // scatterplot, line, bar
            x: 'cycleTime',
            y: 'effort',
            color: 'team',
            size: 'count'
        });
chart.renderTo('#scatter'); // HTML element with 'scatter' id
```
The `renderTo` method will accept one parameter: either a CSS selector or a DOM element.

As a result, you will have the chart like that:

[example jsFiddle](http://jsfiddle.net/taucharts/6m31vccv/)


Currently supported chart types: [scatterplot](scatterplot.md), [line](line.md), [bar](bar.md)

