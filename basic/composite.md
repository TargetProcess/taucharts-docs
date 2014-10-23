## Composite charts

TauCharts API focused on flexible composition architecture instead of rich taxonomy of chart types like many other libraries.

Such an approach allows to build a facet charts by nesting coordinates into coordinates recursively as well as display many different elements (e.g. points, bars, lines) on the chart grid.

Once you understand the composition principles you can build even a facet of facets of facets if you find such a visualization useful.

There are 2 ways of composition supported:
1. Composition in depth. You can insert COORDS.RECT into COORDS.RECT to get a facet chart.
2. Horizontal composition. The API allows to display several chart elements on one grid. Separate axes and shared common axes are possible.

First type of charts is explained in details in [Facets](../basic/facet.html) chapter.

Let's focus on second type. The COORDS.RECT item has *unit* property. It can contain an array of nested elements (points, lines, nested coordinates etc.)

#### Example 1: Several elements on same data

In this example we create coordinate grid and draw same dimensions with different elements (point, line, bar) in parallel. Note how *x* and *y* params are inherited from parent unit if not declared.

```javascript
{
    dimensions: {
        month: { type: 'category' },
        project: { type: 'category' },
        team: { type: 'category' },
        cycleTime: { type: 'measure' },
        effort: { type: 'measure' },
        count: { type: 'measure' }
    },
    unit: {
        type: 'COORDS.RECT',
        guide: {
            padding: { l:56, b:32, r:8, t:8 },
            showGridLines: 'xy',
            x: {label: 'Month'},
            y: {label: { text: 'Count', padding: 36 }}
        },
        x: 'month',
        y: 'count',
        unit: [
            {
                type: 'ELEMENT.POINT'
                // NOTE: "x" and "y" are  inherited from parent unit
            },
            {
                type: 'ELEMENT.INTERVAL',
                x: 'month'
                // NOTE: "y" is inherited from parent unit
            },
            {
                type: 'ELEMENT.LINE',
                x: 'month',
                y: 'count'
            }
        ]
    }
}

```

#### Example 2: Several elements on different data

Let's build a visualization to compare some characteristics for different cars (e.g. CO2 emission and horse power).

Here we create empty COORDS.RECT item to use it as a top composition container and insert 2 coordinates inside. First for CO2 values and second for horse power.

```javascript
{
    dimensions: {
        car: { type: 'category' },
        co2: { type: 'measure' },
        hp : { type: 'measure' }
    },
    unit: {
        type: 'COORDS.RECT',
        // NOTE: "x" and "y" are not specified
        unit: [
            {
                type: 'COORDS.RECT',
                guide: {
                    showGridLines: 'xy',
                    padding: { l:72, b:224, r:8, t:8 },
                    y: {label: { text: 'CO2 emission', padding:52}, tickMin: 0, tickMax: 100},
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
                    showGridLines: 'xy',
                    padding: { l:72, b:224, r:8, t:8 },
                    y: {label: 'Horse power', tickMin: 0, tickMax: 100},
                    x: {rotate: 45, textAnchor: 'start'}
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
