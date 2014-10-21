#What is a facet chart

The Grammar of Graphics provides the following description of the *facet* term:

> The facet implies a little face, such as one of the sides of an object (e.g., a cut diamond) that has many faces. The word is useful for describing an object that creates many little graphics that are variations of a single graphic. In a graphical system, facets are frames of frames. Because of this recursion, facets make frames behave like points in the sense that the center of a frame can be located by coordinates derived from a facet. Thus we can use facets to make graphs of graphs or tables of graphs


IMG

To construct facets we should use coordinates recursively by embedding COORDS.RECT units inside each other.

#Examples

```
var plot = new tauChart.Plot({
    data: [
        { name: "John", age: 30, tshirt: 'M', gender: 'Male',   hasChild: true  },
        ...
        { name: "Jane", age: 28, tshirt: 'L', gender: 'Female', hasChild: true }
    ],
    spec: {
        unit: {
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
                            type: 'ELEMENT.POINT'
                        }
                    ]
                }
            ]
        }
    }
});
```

[example jsBin](http://jsbin.com/wuyujeroxo/1/embed?output&height=500px)
