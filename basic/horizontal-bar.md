
Horizontal bar chart is very easy to create as well. Here is the datasource:

```javascript
var defData = [
        {"team": "d", "cycleTime": 1, "effort": 1, "count": 1, "priority": "low"},
        ...
        {"team": "k", "cycleTime": 4, "effort": 6, "count": 8, "priority": "medium"}];
```

Now just specify 'horizontalBar' type to create a bar chart:

```javascript
var chart = new tauChart.Chart({
            data: defData,
            type: 'horizontalBar',
            x: 'effort',
            y: 'team'
        });
chart.renderTo('#bar');
```

[example jsBin](http://jsbin.com/hogoci/39/embed?output&height=500px)


To define color settings check [encoding](../advanced/encoding.md) section.

Bellow chart has color parameters for encoding group
```javascript
var chart = new tauChart.Chart({
            data: defData,
            type: 'horizontalBar',
            x: 'effort',
            y: 'team',
            color:'priority'
        });
chart.renderTo('#bar');
```
[example jsBin](http://jsbin.com/hogoci/37/embed?output&height=500px)
