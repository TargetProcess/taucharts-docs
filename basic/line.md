For creating line chart you can use
```javascript
var chart = new tauChart.Chart({
            data: defData,
            type: 'line',
            x: 'cycleTime',
            y: 'effort',
            color: 'team'
        });
chart.renderTo('#line');
```
[example jsBin](http://jsbin.com/hogoci/15/embed?output&height=500px)

Color settings see [encoding](../advanced/encoding.md)