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
[example jsBin](http://jsbin.com/hogoci/14/watch?output)

Color settings see [encoding](/advanced/encoding.md)