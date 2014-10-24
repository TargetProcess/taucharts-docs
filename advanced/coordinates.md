##Coordinates

Coordinates is a basic building element in TauChart specification.

There are many types of coordinates:
* Cartesian
* Polar
* Parallel
* Polar parallel
* Triangular (Barycentric)
* Spherical
* Cylindrical
* Local / Global Maps
* 3D
* etc.

For now TauCharts supports Cartesian coordinates only - the most popular coordinate system.

In TauCharts cartesian coordinates are specified using *COORDS.RECT* type:

```javascript
{
    type: "COORDS.RECT"
    ...
    unit: [...]
}
```

You can embed coordinate element inside coordinate element recursively to build a [Facet plot](../basic/facet.md).

Also coordinate element is a container for geometry elements like point or line. Use *unit* property to compose elements:

```javascript
{
    type: "COORDS.RECT"
    ...
    unit: [
        {
            type: "ELEMENT.POINT"
        },
        {
            type: "ELEMENT.LINE"
        }
    ]
}
```

Coordinate element has a rich visual guide settings. [Check them out](../basic/guide.md).
