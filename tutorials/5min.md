If you didn't check [1 minute tutorial](1min), please go and read it. We will not repeat these basics here.

##What is TauCharts?

##How to create a simple scatterplot chart?

This time we will create slightly more compelx chart with some additional visual customizations. Here is out data:


```javascript
var defData = [
        {"team": "d", "cycleTime": 1, "effort": 1, "count": 1, "priority": "low"},
        ...
        {"team": "k", "cycleTime": 4, "effort": 6, "count": 8, "priority": "medium"}];
```

Now we define a scatterplot chart. We use [guide](../basic/guide.md) parameter to define some visual settings like axes labels, overall paddings and colors for the various categories.


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
            color: 'team', // every team will be represented by different color
            size: 'count'
        });
```

[Example jsBin](http://jsbin.com/tohujobuba/1/embed?output&height=500px)

##Work with plugins
Plugins are under construction. So we can do nothing about that. Sad.

##Facets: complex and cool
In TauCharts facet charts group variables using X and Y coordinates. Facet charts help to compare information with many variables.

Most of other javascript charting frameworks doesn't support this type of charts.

The more complex charts demands more complex definition here. You [read about TauCharts language](../advanced/tauchartslanguage.md) in more details.

Basically, we define *units* that will be plotted on a chart and nest them inside each other. Here is a quick example of a facet chart. In this case we have two X axes (gender and age) and two Y axes (hasChild and tshirt). As a result, we have a matrix:


```javascript
var plot = new tauChart.Plot({
    data: [
        { name: "John", age: 30, tshirt: 'M', gender: 'Male',   hasChild: true },
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

[Example jsBin](http://jsbin.com/wuyujeroxo/1/embed?output&height=500px)

Now we recommend to play with TauCharts and read some additional sections about [Basic concepts](../images/guide.png), then jump into [Advanced topics](../advanced/tauchartslanguage.md).
