#What is a facet chart

The Grammar of Graphics provides the following description of the *facet* term:

> The facet implies a little face, such as one of the sides of an object (e.g., a cut diamond) that has many faces. The word is useful for describing an object that creates many little graphics that are variations of a single graphic. In a graphical system, facets are frames of frames. Because of this recursion, facets make frames behave like points in the sense that the center of a frame can be located by coordinates derived from a facet. Thus we can use facets to make graphs of graphs or tables of graphs

Simply speaking, in TauCharts facet charts group variables using X and Y coordinates. Facet charts help to compare information with many variables. You can use various combinations of axes to have just a single row: Y, X, X or a single column: Y, Y, X.

Here is an example of a facet chart. As you see, there are 4 variables encoded using X and Y coordinates. First, on Y axis we see Teams and every small chart Y axis shows how many entities each team completed. X axis shows projects (TP and TP3) and then months.

![An example of facet chart](../images/facet.png)


#How to create a facet chart

To construct facets we should use coordinates recursively by embedding COORDS.RECT units inside each other.

#Examples

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
                    y: {label: 'CO2 emission, g/km'},
                    x: {label: 'Horse power'}
                },
                y: 'co2',
                x: 'hp',
                unit: [
                    {type: 'ELEMENT.POINT'}
                ]
            }
        ]
    }
}
```

[example jsBin](http://jsbin.com/fiwaxetevu/2/embed?output&height=500px)
