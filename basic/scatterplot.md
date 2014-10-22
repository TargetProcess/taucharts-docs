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
[example jsBin](http://jsbin.com/hogoci/16/embed?output&height=500px)
Check [encoding](../advanced/encoding.md#custom-colors-for-encoding-color-value#custom-colors-for-encoding-color-value) section to see how to apply colors.
Use [guide](guide.md) property for some advanced  settings.

Next chart use custom color `'color-red'`,`'color-green'`,`'color-blue'` ang guide property
```javascript
var chart = new tauChart.Chart({
            guide:{
              x:{label:'My x label'},
              y:{label:'My y label'},
              padding:{b:40,l:40,t:10,r:10},
              color:{
                brewer:['color-red', 'color-green', 'color-blue']
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
[example jsBin](http://jsbin.com/hogoci/26/embed?output&height=500px)

