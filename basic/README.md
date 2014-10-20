For creating simple chart you can use.
```javascript
var chart = new tauChart.Chart({
            data: defData,
            type: 'scatterplot',
            x: 'cycleTime',
            y: 'effort',
            color: 'team',
            size: 'count'
        });
chart.renderTo('#scatter');```
Where type can be [scatterplot](scatterplot.md), [line](line.md), [bar](bar.md)


[example jsBin](http://jsbin.com/hogoci/16/embed?output)