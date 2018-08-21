For creating scatterplot chart you can use the following script:

```javascript
var chart = new Taucharts.Chart({
            data: defData,
            type: 'scatterplot',
            x: 'cycleTime',
            y: 'effort',
            color: 'team',
            size: 'count'
        });
chart.renderTo('#scatter');
```
[example jsFiddle](https://jsfiddle.net/taucharts/6LzefLo4/84/)

Check [encoding](../advanced/encoding.md#custom-colors-for-encoding-color-value#custom-colors-for-encoding-color-value) section to see how to apply colors.

Use [guide](guide.md) property for some advanced  settings. Here is an example that sets custom labels for axes and custom colors `'color-red'`,`'color-green'`,`'color-blue'` for elements.

JavaScript

```javascript
var chart = new Taucharts.Chart({
            guide: {
              x: {label:'Cycle Time in days'},  // custom label for X axis
              y: {label:'Effort in points'},    // custom label for Y axis
              padding: {b:40,l:40,t:10,r:10},   // chart paddings
              color: {                          // custom colors
                brewer: ['color-red', 'color-green', 'color-blue']
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

CSS

```css
  .tau-chart__legend__guide--color.color-red,
  .color-red {
    fill: red;
    background-color: red;
  }

  .tau-chart__legend__guide--color.color-green,
  .color-green {
    fill: green;
    background-color:green;
  }

  .tau-chart__legend__guide--color.color-blue,
  .color-blue {
    fill: blue;
    background-color:blue;
  }

```

[example jsFiddle](https://jsfiddle.net/taucharts/bk5Lj66y/31/)
