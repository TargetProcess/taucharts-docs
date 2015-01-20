
Bar chart is very easy to create as well. Here is the datasource:

```javascript
var defData = [
        {"team": "d", "cycleTime": 1, "effort": 1, "count": 1, "priority": "low"},
        ...
        {"team": "k", "cycleTime": 4, "effort": 6, "count": 8, "priority": "medium"}];
```

Now just specify 'bar' type to create a bar chart:

```javascript
var chart = new tauChart.Chart({
            data: defData,
            type: 'bar',
            x: 'team',
            y: 'effort'
        });
chart.renderTo('#bar');
```

[example](http://jsfiddle.net/taucharts/ryaobh0w/)


To define color settings check [encoding](../advanced/encoding.md) section.

Bellow chart has color parameters for encoding group
```javascript
var chart = new tauChart.Chart({
            data: defData,
            type: 'bar',
            x: 'team',
            y: 'effort',
            color:'priority'
        });
chart.renderTo('#bar');
```
[example](http://jsfiddle.net/taucharts/6mdLrj6o/)
