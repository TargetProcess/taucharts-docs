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
[example jsBin](http://jsbin.com/hogoci/7/embed?output&height=500px)

Color settings see [encoding](../advanced/encoding.md)