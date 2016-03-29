# Tooltip

Tooltip plugin allows to explore the data behind visual element. For example, each point on a scatter plot corresponds to a row of data.

By default the plugin displays all properties from the data row.

Here is a code to apply plugin:

```javascript
{
    type: 'scatterplot',
    ...
    plugins: [
        tauCharts.api.plugins.get('tooltip')()
    ]
}
```

## Tooltip settings

There are some settings to customize a tooltip behavior.

#### fields

By default the plugin displays all properties from the data row.

The **fields** property allows to specify which properties from a row to show on a tooltip.

```javascript
{
    type: 'scatterplot',
    x: 'weight',
    y: 'height',
    color: 'gender',
    data: [
        {weight: 65, height: 170, gender: 'male',   age: 25, name: 'Konstantin'},
        ...
        {weight: 50, height: 160, gender: 'female', age: 18, name: 'Ann'}
    ],
    plugins: [
        tauCharts.api.plugins.get('tooltip')({
            // will see only name and age on tooltip
            fields: ['name', 'age']
        })
    ]
}
```

#### formatters

By default the plugin formats displayed properties according to a chart guide or leaves them as is.

The **formatters** property allows to rename displayed property name and specify format for property value.

It is a hash object where key is a name of original property and value is a *{label, format}* object:

* The **label** (*string*) allows to rename default property name
* The **format** (*function* or [*d3 format string*](https://github.com/mbostock/d3/wiki/Formatting)) allows to specify formatter for property value.

```javascript
{
    type: 'scatterplot',
    x: 'weight',
    y: 'height',
    color: 'gender',
    guide: {
        x: {label: "Person Weight"},
        y: {label: "Bla bla Height"}
    },
    data: [
        {weight: 65, height: 170, gender: 'male',   age: 25, name: 'Konstantin'},
        ...
        {weight: 50, height: 160, gender: 'female', age: 18, name: 'Ann'}
    ],
    plugins: [
        tauCharts.api.plugins.get('tooltip')({
            // will see only name and age on tooltip
            formatters: {
                // weight will be displayed as                // Person Weight: 50
                age: {label: "Person Age", format: "03d"},    // Person Age   : 018
                height: {
                    label: "Person Height",
                    format: function (n) {
                        return (n + " cm");                   // Person Height: 160 cm
                    }
                },
                // (!) short notation
                name: function (str) {
                    return str.toUpperCase();                 // name         : ANN
                }
            }
        })
    ]
}
```

Once you don't want to change displayed property name there is a short notation. Instead of the a *{label / format}* object - specify value formatter directly.