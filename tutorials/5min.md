If you didn't check [1 minute tutorial](1min), please go and read it. We will not repeat these basics here.

##What is TauCharts?

##How to create a simple scatterplot chart?

```javascript
var chart = new tauChart.Chart({
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

##Work with plugins

##Facets: complex and cool
In TauCharts facet charts group variables using X and Y coordinates. Facet charts help to compare information with many variables.

Most of other javascript charting frameworks doesn't support this type of charts.

Here is a quick example:


```javascript
var plot = new tauChart.Plot({
    data: [
        { name: "John", age: 30, tshirt: 'M', gender: 'Male',   hasChild: true  },
        ...
        { name: "Jane", age: 28, tshirt: 'L', gender: 'Female', hasChild: true }
    ],
    spec: {
        unit: { // outer X and Y axes
            type: 'COORDS.RECT',
            x: 'gender',
            y: 'hasChild',
            unit: [
                {
                    type: 'COORDS.RECT',
                    x: 'age',
                    y: 'tshirt',
                    unit: [
                        {
                            type: 'ELEMENT.POINT' // scatterplot
                        }
                    ]
                }
            ]
        }
    }
});
```


[xample jsBin](http://jsbin.com/wuyujeroxo/1/embed?output&height=500px)
