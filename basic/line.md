Let's create a simple line chart.

TODO: change example to something more relevant. For example, how average CycleTime changes for 3 teams with time.

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

Use [guide](guide.md) property for visual settings.

TODO: Example with guide

[example jsBin](http://jsbin.com/hogoci/15/embed?output&height=500px)
