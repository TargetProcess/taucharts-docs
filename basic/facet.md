#What is a facet chart

The Grammar of Graphics provides the following description of the *facet* term:

> The facet implies a little face, such as one of the sides of an object (e.g., a cut diamond) that has many faces. The word is useful for describing an object that creates many little graphics that are variations of a single graphic. In a graphical system, facets are frames of frames. Because of this recursion, facets make frames behave like points in the sense that the center of a frame can be located by coordinates derived from a facet. Thus we can use facets to make graphs of graphs or tables of graphs

Simply speaking, in TauCharts facet charts group variables using X and Y coordinates. Facet charts help to compare information with many variables. You can use various combinations of axes to have just a single row: Y, X, X or a single column: Y, Y, X.

Here is an example of a facet chart. As you see, there are 4 variables encoded using X and Y coordinates. First, on Y axis we see Teams and every small chart Y axis shows how many entities each team completed. X axis shows projects (TP and TP3) and then months.

![An example of facet chart](../images/facet.png)


#How to create a facet chart

To construct facets we should use coordinates recursively by embedding COORDS.RECT units inside each other.

#Examples

TODO: Replace with a better data

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

[example jsBin](http://jsbin.com/wuyujeroxo/1/embed?output&height=500px)
