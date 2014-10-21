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

Check [encoding](../advanced/encoding.md#custom-colors-for-encoding-color-value#custom-colors-for-encoding-color-value) section to see how to apply colors.

TODO: simple color example

Use [guide](guide.md) property for some advanced  settings.

TODO: simple guide example

[example jsBin](http://jsbin.com/hogoci/16/embed?output&height=500px)
