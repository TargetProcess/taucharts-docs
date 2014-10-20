For creating scatterplot chart you can use
```javascript
var chart = new tauChart.Chart({
            data: defData,
            type: 'scatterplot',
            x: 'cycleTime',
            y: 'effort',
            color: 'team',
            size: 'count'
        });
chart.renderTo('#scatter');
```
Scatterplot chart is wrapper over a [point element](../advanced/elements.md#point) and has same settings.
Color settings see [encoding](../advanced/encoding.md)
[example jsBin](http://jsbin.com/hogoci/16/embed?output&height=500px)
