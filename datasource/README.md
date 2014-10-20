##Data source

You can think of TauCharts API as a mapping between data variable set (data dimensions) and visual encoding parameters (X, Y, color and size).

```javascript
var plot = new tauCharts.Chart({
    // data dimensions
    data: [
        { name: "John", age: 30, gender: 'Male',   hasChild: true  },
        ...
        { name: "Mary", age: 22, gender: 'Female', hasChild: false }
    ],
    type:  "scatterplot",
    ...
    // visual encoding 
    x:     "gender",
    y:     "age",
    size:  "age",
    color: "hasChild"
});
```

[example jsBin](http://jsbin.com/hazelanari/2/embed?output&height=500px)

TauCharts requires the source data to be provided in a form of structured table which can be expressed in javascript as an array of same-typed objects (e.g. in example above: name, age, gender, hasChild).

By default TauCharts try to detect a dimension type which can be categorical, qualitative or quantitative.

* Categorical: Represents data that can't be compared. Let's say, list of countries or names.
* Qualitative: Can be ordered, but you can't say how bigger one value from the other. For example, you can say that Must Have is more important than Nice to Have, but you can't say that Must Have is twice as important.
* Quantitative: That is easy. You can compare these variables, add them, multiply them, etc.

Also you can explicitly specify dimension type within *dimensions* section:

```javascript
var plot = new tauCharts.Chart({
    data: [
        { name: "John", age: 30, gender: 'Male',   hasChild: true  },
        ...
        { name: "Mary", age: 22, gender: 'Female', hasChild: false }
    ],
    dimensions: {
        name: { type: 'categorical', scale: 'ordinal' },
        age: { type: 'quantitative' },
        gender: { type: 'categorical' },
        hasChild: { type: 'categorical' }
    },
    type:  "scatterplot",
    ...
    x:     "gender",
    y:     "age",
    size:  "age",
    color: "hasChild"
});
```

## Nested objects in DataSource


```javascript
{
    data: [
        { name: "John", gender: { key: 1, value: 'Male'  }},
        ...
        { name: "Mary", gender: { key: 2, value: 'Female'}}
    ],
    dimensions: {
        ...
        gender: {
            type: 'categorical',
            value:   'key'
            
        }
        ...
    },
    ...
});
```


## Sorting data

You can specify sort order for dimension domain using [ASC | DESC] keywords (thet are case insensitive, in fact).

```javascript
dimensions: {
    name: { scale: 'ordinal', sort: 'DESC' }
    ...
}
```


##### Qualitative data handling

Using this method you should declare data property as a string but provide to dimension declaration an [index] array which is an ordered list of available categories. Once you have in data some unknown categories they will be added to the tail of [index] in unknown order.

The [index] specifies ascending order for categories.

```javascript
{
    data: [
        { name: "John", tshirt: 'S'},
        ...
        { name: "Mary", tshirt: 'M'},
        ...
        { name: "Pete", tshirt: 'XXXXL'}
    ],
    dimensions: {
        ...
        tshirt: {
            scale: 'ordinal',
            index: ['S', 'M'],
            sort: 'DESC'
        }
        ...
    },
    ...
});
```

[example jsBin](http://jsbin.com/beqalufomi/1/embed?output&height=500px)

NOTE: Specifying sort order for quantitative dimension doesn't make any effect since such dimensions are always displayed in ascending order.
