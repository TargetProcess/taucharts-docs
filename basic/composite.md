## Composite charts

TauCharts API focuses on flexible composition architecture instead of rich taxonomy of chart types like many other libraries.

This approach allows to build a facet charts by nesting coordinates into coordinates recursively as well as display many different elements (e.g. points, bars, lines) on the chart grid.

When you understand the composition principles, you can build even a facet of facets of facets if you find such a visualization useful.

There are 2 ways of composition supported:
1. Composition in depth. You can insert COORDS.RECT into COORDS.RECT to get a facet chart.
2. Horizontal composition. API allows to display several chart elements on one grid. It means that separate axes and shared common axes are possible.

[Facets](../basic/facet.html) are explained in another chapter. So let's focus on the second type.

#### Example 1: Share axis

Let's visualy compare several numerical properties of the dataset. The Taucharts at the moment doesn't have special syntax for the task but there is a workaround. We need to introduce new variables to the data which transform meta-data to a format that Taucharts can operate with.

```javascript
var co2_vs_hp_by_cars_chart = new tauCharts.Chart({

    "type": "line",
    "x": ["car"],
    "y": ["co2,hp"],
    "color": "co2-hp-type",

    data: [
            {car: "BMV X5", co2: 197, hp: 306},
            {car: "Bentley Continental", co2: 246, hp: 507},
            {car: "Infinity FX", co2: 238, hp: 238},
            {car: "Toyota Prius+", co2: 96, hp: 99},
            {car: "Mercedes Vito", co2: 203, hp: 95},
            {car: "Peugeot 3008", co2: 155, hp: 120},
            {car: "Volvo S60", co2: 135, hp: 150},
            {car: "Subaru Forester", co2: 186, hp: 150},
            {car: "Lexus RX", co2: 233, hp: 188}
          ].reduce(function (memo, row) {

                var keyVal = "co2,hp";
                var keyType = "co2-hp-type";

                var r1 = _.clone(row);
                r1[keyType] = 'co2';
                r1[keyVal] = row['co2'];

                var r2 = _.clone(row);
                r1[keyType] = 'hp';
                r2[keyVal] = row['hp'];

                return memo.concat([r1, r2]);
            }, [])
});
```

Here we double source array by generating a new record for each property (i.e co2 and hp) and introduce two new variables "co2,hp" and "co2-hp-type". This is some kind of "unpacking meta-data". The "co2,hp" variable become a new composite axis while "co2-hp-type" variable is used to split geoms by color. 

[example](http://jsfiddle.net/cdmjp86t/10/)

#### Example 2: Visual experiments

While "Example 1" should cover 80% of the needs there is a lot of flexibility inside Taucharts DSL to support a special cases.

#####NOTE: at the moment DSL syntax is not stable enough so the following examples are experimental and you can use them on your own risk. At the same time we are working to provide shortcuts for popular "special cases".

What if I don't want to merge domain for "hp" and "co2" variables from the example above? The Taucharts DSL is flexible enough to draw two or more axes for cartesian coordinates. In this example we use several data sources to create two types of cartesian coordinates. One serves as a layout for coordinates composition while the rest represents data itself.

[example](http://jsfiddle.net/bjwLaem1/8/)

Also we can merge layout cells and use padding guide to save both axes while visually "share" coordinates canvas.

[example](http://jsfiddle.net/7tbjnhbj/5/)




