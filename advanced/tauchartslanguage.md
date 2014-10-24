## TauChart language

The flexibility of TauChart library is powered by charts intermediate language (CIL) which is inspired by Leland Wilkinson's work "Grammar of Graphics".

CIL is a declarative language which describes the following aspects:
* Structure of data source (meta data)
    * data dimensions (variable names)
    * type of dimensions (category | order | measure)
    * which scale to use for dimension by default (ordinal, linear, logarithmic)
* Logical structure and data mappings:
    * how to map data source variables to plot structure and other visual encoding parameters
    * which type of coordinates to use (COORDS.RECT)
    * which data source variables to use as X, Y axes
    * which geometry to use on plot (ELEMENT.POINT, ELEMENT.LINE, etc)
    * how to encode geometry attributes (color, size, etc) by data source variables
    * how to compose coordinates grid and geometry elements within logical plot structure (to get facet or a set of plots)
* Layout
    * visual encoding settings (e.g. color brewers)
    * layout markup settings (paddings, text rotation, etc)
    * axes labels / visibility / paddings

In the heart of CIL a decomposition of any plot structure on the following items:
* Coordinates (COORDS)
* Geometry (ELEMENTs)

It can be described as:

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

This syntax allows to describe logical plot structure.

Then logical structure can be visually decorated with some pre-defined layout parameters. In CIL we use *guide* property for this purpose:

```javascript
{
    type: 'COORDS.RECT',
    guide: {
        ...
        padding: { l:120, b:4, r:8, t:4 },
        showGridLines: 'xy',
        y: {label: 'Cycle Time', tickMin: 0, tickMax: 100}
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

By default sub element inherits parent properties like x, y, guide.


## Rendering Process

Let's make an overview of the process which transforms declarative specification to visual plot.

There are 3 main steps:

1. **Build logical structure**. TauChart plot engine expands CIL specification to tree  structure based on data domain.
2. **Calculate Layout**. On this step layout engine traverses tree structure and calculates phisical position and size for each item to fit the plot into the given area.
3. **Draw**. On this stage the engine traverses the layout tree from previous step and calls drawer for each item with corresponding configuration.

The division by these stages allows to control the process and augment behavior on each step using plugins.
