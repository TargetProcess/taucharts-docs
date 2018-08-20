
Bar chart is very easy to create as well. Here is the datasource:

```javascript
var defData = [
        {"team": "One", "cycleTime": 1, "effort": 1, "count": 1, "priority": "low"},
        ...
        {"team": "Two", "cycleTime": 4, "effort": 6, "count": 8, "priority": "medium"}];
```

Now just specify 'bar' type to create a bar chart:

```javascript
var chart = new Taucharts.Chart({
            data: defData,
            type: 'bar',
            x: 'team',
            y: 'effort'
        });
chart.renderTo('#bar');
```

[example](https://jsfiddle.net/taucharts/ryaobh0w/330/)


To define color settings check [encoding](../advanced/encoding.md) section.

The chart below has color parameters for encoding group
```javascript
var chart = new Taucharts.Chart({
            data: defData,
            type: 'bar',
            x: 'team',
            y: 'effort',
            color:'priority'
        });
chart.renderTo('#bar');
```
[example](https://jsfiddle.net/taucharts/6mdLrj6o/229/)
