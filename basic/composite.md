## Composite charts

TauCharts API focuses on flexible composition architecture instead of rich taxonomy of chart types like many other libraries.

This approach allows to build a facet charts by nesting coordinates into coordinates recursively as well as display many different elements (e.g. points, bars, lines) on the chart grid.

When you understand the composition principles, you can build even a facet of facets of facets if you find such a visualization useful.

There are 2 ways of composition supported:
1. Composition in depth. You can insert COORDS.RECT into COORDS.RECT to get a facet chart.
2. Horizontal composition. API allows to display several chart elements on one grid. It means that separate axes and shared common axes are possible.

[Facets](../basic/facet.html) are explained in another chapter. So let's focus on the second type. The [COORDS.RECT](../advanced/coordinates.md) item has *unit* property. It can contains an array of nested [elements](../advanced/elements.md) (points, lines, nested coordinates etc.)

#### Example 1: Several elements on same data

In this example we create coordinate grid and draw same dimensions with different elements (point, line, bar) in parallel. Note how *x* and *y* params are inherited from parent unit if not declared.

```javascript
{
    dimensions: {
        car: {type: 'category'},
        co2: {type: 'measure'},
        hp: {type: 'measure'}
    },

    unit: {
        type: 'COORDS.RECT',
        guide: {
            showGridLines: '',
            padding: {l: 72, b: 120, r: 8, t: 8},
            // NOTE: use tickMin / tickMax to specify values range
            y: {label: 'Horse power'},
            x: {rotate: 45, textAnchor: 'start'}
        },
        x: 'car',
        y: 'hp',
        unit: [
            {type: 'ELEMENT.INTERVAL'},
            {type: 'ELEMENT.POINT'},
            {type: 'ELEMENT.LINE'}
        ]
    }
}
```
[example jsBin](http://jsbin.com/lokoxomape/1/embed?output&height=500px)

#### Example 2: Several elements on different data

Let's build a visualization to compare some characteristics for different cars (e.g. CO<sub>2</sub> emission and horse power).

Here we create empty COORDS.RECT item to use it as a top composition container and insert 2 coordinates inside. First bar chart for CO<sub>2</sub> values and second line chart for horse power. Note how we use *guide/split* flag to draw nested coordinates separately, CO<sub>2</sub> above hp.

```javascript
{
    dimensions: {
        car: { type: 'category' },
        co2: { type: 'measure' },
        hp : { type: 'measure' }
    },

    unit: {
        type: 'COORDS.RECT', // top container
        guide: { split: true },
        unit: [
            {
                type: 'COORDS.RECT',
                guide: {
                    showGridLines: 'xy',
                    padding: { l:72, b:4, r:8, t:8 },
                    y: {label: 'CO2 emission, g/km'},
                    x: {hide: true}
                },
                x: 'car',
                y: 'co2',
                unit: [
                    {type: 'ELEMENT.INTERVAL'}
                ]
            },
            {
                type: 'COORDS.RECT',
                guide: {
                    showGridLines: 'xy',
                    padding: { l:72, b:124, r:8, t:8 },
                    y: {label: 'Horse power'},
                    x: {rotate: 50, textAnchor: 'start'}
                },
                x: 'car',
                y: 'hp',
                unit: [
                    {type: 'ELEMENT.POINT'},
                    {type: 'ELEMENT.LINE'}
                ]
            }
        ]
    }
}
```

[example jsBin](http://jsbin.com/ninalevedi/2/embed?output&height=500px)

But what if you want to draw both bar and line on one grid? In this case you have to share Y axis for both charts. To do that we need to normalize the axis to common values domain by using *tickMin* / *tickMax* properties and set *guide/split* flag to *false* (actually *false* is default value).

```javascript
{
    dimensions: {
        car: {type: 'category'},
        co2: {type: 'measure'},
        hp: {type: 'measure'}
    },

    unit: {
        type: 'COORDS.RECT',
        guide: {split: false},
        unit: [
            {
                type: 'COORDS.RECT',
                guide: {
                    showGridLines: 'xy',
                    padding: {l: 72, b: 224, r: 8, t: 8},
                    // NOTE: use tickMin / tickMax to specify values range
                    y: {label: {text: 'CO2 emission, g/km', padding: 52}, tickMin: 0, tickMax: 600},
                    x: {rotate: 90, textAnchor: 'start', hide: true}
                },
                y: 'co2',
                x: 'car',
                unit: [
                    {type: 'ELEMENT.INTERVAL'}
                ]
            },
            {
                type: 'COORDS.RECT',
                guide: {
                    showGridLines: '',
                    padding: {l: 72, b: 224, r: 8, t: 8},
                    // NOTE: use tickMin / tickMax to specify values range
                    y: {label: 'Horse power (red line)', tickMin: 0, tickMax: 600},
                    x: {rotate: 45, textAnchor: 'start'},
                    color: { brewer: ['color-red'] }
                },
                x: 'car',
                y: 'hp',
                unit: [
                    {type: 'ELEMENT.POINT'},
                    {type: 'ELEMENT.LINE'}
                ]
            }
        ]
    }
}
```

[example jsBin](http://jsbin.com/girubegara/2/embed?output&height=500px)




