Let's create a simple line chart.

For example, count of entities was completed by month.
Red line show bugs and blue line show user story on graphics. Certain color by type entity describe in guide property.
```javascript
var chart = new tauChart.Chart({
    guide: {
        padding: {l: 70, t: 10, b: 70, r: 10},
        showGridLines: 'xy',
        color: {
            brewer: {
                us: 'color-us',
                bug: 'color-bug'
            }
        },
        y: {
            label: {
                text: 'Count of completed entities',
                padding: 50
            }
        },
        x: {
            label: 'Month'
        }
    },
    data: defData,
    type: 'line',
    x: 'date',
    y: 'count',
    color: 'type'
});

chart.renderTo('#line');

```

Use [guide](guide.md) property for visual settings.

[example jsBin](http://jsbin.com/hogoci/29/embed?output&height=500px)
