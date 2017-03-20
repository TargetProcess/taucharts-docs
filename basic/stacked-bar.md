Stacked bar chart shows a grouped structure in the data it represents. It is good for comparing relation of part to whole and between other parts.

Let's take the sample data of sales:

```javascript
var data = [
    { process: 'sales', stage: 'visit', count: 100 },
    { process: 'sales', stage: 'trial', count: 50  },
    { process: 'sales', stage: 'buy',   count: 15  },
    { process: 'sales', stage: 'away',  count: -7  }
];
```
To create a stacked bar - use 'stacked-bar' type in chart definition:

```javascript
var chart = new tauCharts.Chart({
    type: 'stacked-bar',
    x   : 'process',
    y   : 'count',
    data: data
});
```

[example](https://jsfiddle.net/eawan9ym/2/)

Now let's encode each stage with color for better visibility:

```javascript
var chart = new tauCharts.Chart({
    type : 'stacked-bar',
    x    : 'process',
    y    : 'count',
    color: 'stage',
    data : data
});
```
[example](https://jsfiddle.net/eawan9ym/3/)

Also each part of stacked bar chart might be encoded with size. This can be useful to produce funnel-like plots:

```javascript
var chart = new tauCharts.Chart({
    type : 'stacked-bar',
    x    : 'process',
    y    : 'count',
    color: 'stage',
    size : 'ABS(count)',
    data : data
});
```
[example](https://jsfiddle.net/eawan9ym/4/)

> NOTE: You can stack numeric data only so make sure the variable you map to "y" axis is a number. Otherwise the "Stacked field [...] should be a number" exception is thrown.