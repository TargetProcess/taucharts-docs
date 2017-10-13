## Taucharts language

The flexibility of Taucharts library is powered by Charts Intermediate Language (CIL) which is inspired by Leland Wilkinson's work "Grammar of Graphics".

CIL is a declarative language which describes the following aspects:
* [Data source](../datasource/README.md) structure (meta data)
    * data dimensions (variable names)
    * dimension types (category | order | measure)
    * Default scale for dimension (ordinal, linear, logarithmic)
* Logical structure and data mappings:
    * how to map data source variables to plot structure and other visual encoding parameters
    * which [coordinates](coordinates.md) type use (COORDS.RECT)
    * which data source variables  use as X, Y axes
    * which [geometry](elements.md) to use on a plot (ELEMENT.POINT, ELEMENT.LINE, etc)
    * how to [encode retinal variables](encoding.md) (color, size, etc) by data source variables
    * how to compose coordinates grid and geometry elements within logical plot structure to get facet or a set of plots
* [Layout](../basic/guide.md)
    * visual encoding settings (e.g. color brewers)
    * layout markup settings (paddings, text rotation, etc)
    * axes labels / visibility / paddings

CIL based on a decomposition of any plot structure to the following items:
* [Coordinates](coordinates.md) (COORDS)
* [Geometry](elements.md) (ELEMENTs)

```javascript
{
    type: 'COORDS.RECT'
    ...
}
```
or

```javascript
{
    type: 'ELEMENT.POINT'
    ...
}
```

The *coordinate* item allows recursive composition. In CIL we use *unit* property:

```javascript
{
    type: 'COORDS.RECT'
    unit: [
        {
            type: 'COORDS.RECT',
            unit: [
                {
                    type: 'ELEMENT.POINT'
                    ...
                }
            ]
        }
    ]
}
```

This syntax describes logical plot structure.

Then the logical structure can be visually decorated with some pre-defined layout parameters. In CIL we use [*guide*](../basic/guide.md) property for this purpose:

```javascript
{
    type: 'COORDS.RECT',
    guide: {
        ...
        padding: { l:120, b:4, r:8, t:4 },
        showGridLines: 'xy',
        y: {label: 'Cycle Time', tickMin: 0, tickMax: 100, autoScale: false}
    },
    ...
    unit: [
        {
            type: 'ELEMENT.POINT',
            guide: {
                ...
                y: {tickMin: 0, tickMax: 100}
            }
            ...
        }
    ]
}
```

By default inner element inherits parent properties like x, y, guide.


## Rendering Process

Here is how declarative specification transforms to a visual plot in 3 main steps:

1. **Build logical structure**. Taucharts plot engine expands CIL specification to a tree structure based on data domain.
2. **Calculate Layout**. On this step layout engine traverses tree structure and calculates physical position and size for each item to fit the plot into the given area.
3. **Draw**. On this stage the engine traverses the layout tree from previous step and calls drawer for each item with corresponding configuration.

The division by these stages allows to control the process and augment behavior on each step using [plugins](../plugins/README.md).
