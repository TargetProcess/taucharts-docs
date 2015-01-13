## Scatterplot Matrices (SPLOMs)

The [scatterplot matrix](http://junkcharts.typepad.com/junk_charts/2010/06/the-scatterplot-matrix-a-great-tool.html) (SPLOM) was invented by John Hartigan (1975). The SPLOM replaces the numbers in a covariance or correlation matrix with the scatterplots of the data on which they were computed. In other words, it allows visually search most interesting correlations between parameters in the data set.

Let's check an example. There is a data source with car characteristics:

```javascript
{
    car : "...",
    hp  : 150,  // horse power
    co2 : 238,  // CO2 emission
    mpg : 10    // miles per galon
}
```

We want to know are there any patterns or correlations between parameters (e.g. hp vs. co2, hp vs. mpg, co2 vs. mpg) in the whole data set.

To address this problem, we need to transform data to the format where meta data (property names) becomes a category property:

```javascript
{
    param1: 'co2',
    param2: 'mpg',
    value1: 238,    // CO2 emission
    value2: 10      // miles per galon
}
```

using the following script:

```javascript
sourceArray.reduce(
    function(memo, x) {
        var keyNames = ['hp', 'co2', 'mpg'];
        keyNames.forEach(function(mainParam) {
            keyNames.forEach(function(subParam) {
                memo.push({
                    param1: mainParam,
                    param2: subParam,
                    value1: x[mainParam],
                    value2: x[subParam]
                });
            });
        });
        return memo;
    },
    []
);
```

and build a facet that visualizes correlation. In this case we have three categories, so we will have 3x3 matrix.

```javascript
{
    dimensions: {
        param1: {type: 'category'},
        param2: {type: 'category'},
        value1: {type: 'measure'},
        value2: {type: 'measure'}
    },

    unit: {
        type: 'COORDS.RECT',
        guide: {
            padding: {l: 42, b: 24, r: 8, t: 8}
        },
        x: 'param1', // here we have categories, like mpg
        y: 'param2',
        unit: [
            {
                type: 'COORDS.RECT',
                guide: {
                    showGridLines: 'xy'
                },
                x: 'value1', // here we have exact measures
                y: 'value1',
                unit: [
                    {type: 'ELEMENT.POINT'}
                ]
            }
        ]
    }
}
```

[Example](http://jsfiddle.net/taucharts/814f5caL/)

