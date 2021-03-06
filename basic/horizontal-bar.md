
Horizontal bar chart is very easy to create as well. Here is the datasource:

```javascript
var defData = [
        {"team": "d", "cycleTime": 1, "effort": 1, "count": 1, "priority": "low"},
        ...
        {"team": "k", "cycleTime": 4, "effort": 6, "count": 8, "priority": "medium"}];
```

Now just specify 'horizontal-bar' or 'horizontalBar' type to create a horizontal bar chart:

```javascript
var chart = new Taucharts.Chart({
            data: defData,
            type: 'horizontalBar',
            x: 'effort',
            y: 'team'
        });
chart.renderTo('#bar');
```

[example](https://jsfiddle.net/taucharts/ryaobh0w/331/)


To define color settings check [encoding](../advanced/encoding.md) section.

The chart below has color parameters for encoding group
```javascript
var chart = new Taucharts.Chart({
            data: defData,
            type: 'horizontalBar',
            x: 'effort',
            y: 'team',
            color:'priority'
        });
chart.renderTo('#bar');
```
[example](https://jsfiddle.net/taucharts/6mdLrj6o/236/)
