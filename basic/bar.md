
For creating line chart you can use
```javascript
var chart = new tauChart.Chart({
            data: defData,
            type: 'bar',
            x: 'team',
            y: 'effort'
        });
chart.renderTo('#bar');
```
[example jsBin](http://jsbin.com/hogoci/18/embed?output&height=500px)

Color settings see [encoding](../advanced/encoding.md)

