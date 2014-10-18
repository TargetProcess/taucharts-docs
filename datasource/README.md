##Data source

You can think of TauCharts API as a mapping between data variable set (data dimensions) and visual encoding parameters.

```javascript
var plot = new tauCharts.Chart({
    data: [
        { name: "John", age: 30, gender: 'Male',   hasChild: true  },
        ...
        { name: "Mary", age: 22, gender: 'Female', hasChild: false }
    ],
    spec: {
        type:  "scatterplot",
        ...
        x:     "gender",
        y:     "age",
        size:  "age",
        color: "hasChild"
    }
});
```

![](https://dl.dropboxusercontent.com/u/96767946/tauchart-docs/tauchart-docs-1.png)

According to this conception the API requires source data to be provided in form of structured table which can be expressed in javascript as an array of same-typed objects (e.g. in example above: name, age, gender, hasChild).

NOTE: we plan to support X-Array format in the near future.

By default TauCharts try to detect a dimension type which can be categorical or quantitative.

Also you can explicitly specify dimension type within [spec.dimensions] section:

```javascript
var plot = new tauCharts.Chart({
    data: [
        { name: "John", age: 30, gender: 'Male',   hasChild: true  },
        ...
        { name: "Mary", age: 22, gender: 'Female', hasChild: false }
    ],
    spec: {
        dimensions: {
            name: { scaleDim: 'ordinal' },
            age: { scaleDim: 'linear' },
            gender: { scaleDim: 'ordinal' },
            hasChild: { scaleDim: 'ordinal' }
        },
        type:  "scatterplot",
        ...
        x:     "gender",
        y:     "age",
        size:  "age",
        color: "hasChild"
    }
});
```

You can specify sort order for dimension domain using [ASC | DESC] keywords (non case sensitive).

```javascript
dimensions: {
    name: { scaleDim: 'ordinal', sort: 'DESC' },
    age : { scaleDim: 'linear' , sort: 'Asc' },
    ...
}
```

Non-ordered categorical dimensions will be sorted alphabetically by default.

Ordered categorical dimension should be declared in a special way.

There are 2 variants available:

1. Category as object with id and name.
2. Category as a token in the ordered array.


#####Category as object with id and name

Using this method you should put in data property a nested object and provide mapping for category id (a number) and category name.

Mapping can be declared using:

* strings (first level property names) or
* functions (useful for non-trivial and deep nested properties).

Sorting will be applied by numerical [id] property.

```javascript
{
    data: [
        { name: "John", gender: { key: 1, val: 'Male'  }},
        ...
        { name: "Mary", gender: { key: 2, val: 'Female'}}
    ],
    spec: {
        dimensions: {
            ...
            gender: {
                scaleDim: 'ordinal',
                id:   'key',                // string
                name: function(genderObj) { // function
                    return genderObj.val
                },
                sort: 'Desc'
            }
            ...
        },
        ...
    }
});
```

#####Category as a token in the ordered array

Using this method you should declare data property as a string but provide to dimension declaration an [index] array which is an ordered list of available categories. Once you have in data some unknown categories they will be added to the tail of [index] in unknown order.

The [index] specifies ascending order for categories.

```javascript
{
    data: [
        { task: "Watch TV"       , priority: 'low' },
        ...
        { task: "Visit a dantist", priority: 'high'}
    ],
    spec: {
        dimensions: {
            ...
            priority: {
                scaleDim: 'ordinal',
                index: ['low', 'medium', 'high'],
                sort: 'Desc'
            }
            ...
        },
        ...
    }
});
```
