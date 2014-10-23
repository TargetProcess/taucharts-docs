#What is a facet chart

The Grammar of Graphics provides the following description of the *facet* term:

> The facet implies a little face, such as one of the sides of an object (e.g., a cut diamond) that has many faces. The word is useful for describing an object that creates many little graphics that are variations of a single graphic. In a graphical system, facets are frames of frames. Because of this recursion, facets make frames behave like points in the sense that the center of a frame can be located by coordinates derived from a facet. Thus we can use facets to make graphs of graphs or tables of graphs

Simply speaking, in TauCharts facet charts group variables using X and Y coordinates. Facet charts help to compare information with many variables. You can use various combinations of axes to have just a single row: Y, X, X or a single column: Y, Y, X.

Here is an example of a facet chart. As you see, there are 4 variables encoded using X and Y coordinates. First, on Y axis we see Teams and every small chart Y axis shows how many entities each team completed. X axis shows projects (TP and TP3) and then months.

![An example of facet chart](../images/facet.png)


## How to create a facet chart

To construct facets we should use coordinates recursively by embedding COORDS.RECT units inside each other.

## Example 1: Segmentation

In the following example we use facet chart to visualize distribution of car models among segments powerfull / eco-friendly. While detailed information on horse power and CO2 emission is still available for each segment.

```javascript
{
    dimensions: {
        car: {type: 'category'},
        euroEco: {type: 'category'},
        power: {
            type: 'order',
            order: ['low', 'normal', 'high']
        },
        co2: {type: 'measure'},
        hp: {type: 'measure'}
    },

    unit: {
        type: 'COORDS.RECT',
        guide: {
            split: false,
            padding: {l: 42, b: 24, r: 8, t: 8},
        },
        x: 'euroEco',
        y: 'power',
        unit: [
            {
                type: 'COORDS.RECT',
                guide: {
                    showGridLines: 'xy',
                    padding: {l: 52, b: 42, r: 8, t: 8},
                    x: {label: 'CO2 emission, g/km'},
                    y: {label: 'Horse power'}
                },
                x: 'co2',
                y: 'hp',
                unit: [
                    {type: 'ELEMENT.POINT'}
                ]
            }
        ]
    }
}
```

[example jsBin](http://jsbin.com/zodocuzeco/1/embed?output&height=500px)

## Example 2: Scatterplot Matrices (SPLOMs)

The scatterplot matrix (SPLOM) was invented by John Hartigan (1975). The SPLOM replaces the numbers in a covariance or correlation matrix with the scatterplots of the data on which they were computed. In other words it allows visually search most interesting correlations between parameters in the data set.

Let's consider example. There is a data source with car characteristics:

```javascript
{
    car : "...",
    hp  : 150,  // horse power
    co2 : 238,  // CO2 emission
    mpg : 10    // miles per galon
}
```

We want to know: is there any patterns or correlation between parameters (e.g. hp vs co2, hp vs mpg, co2 vs mpg) on the whole data set?

To address this question we need to transform source data to the format where meta data (property names) becomes a category property:

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

and build a facet which visualize correlation:

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
        x: 'param1',
        y: 'param2',
        unit: [
            {
                type: 'COORDS.RECT',
                guide: {
                    showGridLines: 'xy'
                },
                x: 'value1',
                y: 'value1',
                unit: [
                    {type: 'ELEMENT.POINT'}
                ]
            }
        ]
    }
}
```

[example jsBin](http://jsbin.com/jetowayige/2/embed?output&height=500px)

