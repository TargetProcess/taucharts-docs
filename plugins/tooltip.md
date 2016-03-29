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

### Tooltip settings

There are some settings to customize a tooltip behavior.

### fields

By default the plugin displays all properties from the data row.

The *fields* property allows to specify which properties from a row to show on a tooltip.

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

### formatters

By default the plugin displays all properties from the data row.

The *fields* property allows to specify which properties from a row to show on a tooltip.

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
