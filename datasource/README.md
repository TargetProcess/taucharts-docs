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

By default TauCharts try to detect a dimension type which can be a category, order or measure.

* Category: Represents data that can't be compared. Let's say, list of countries or names.
* Order: As you might guess, represents data taht can be ordered, but you can't say how bigger one value from the other. For example, you can say that Must Have is more important than Nice to Have, but you can't say that Must Have is twice as important.
* Measure: That is easy. You can compare these variables, add them, multiply them, etc.

Basing on dimension type TauChart will try to find most appropriate scale for a dimension. Here is a list of default scales for corresponding dimension types:

| type | scale |
| -- | -- |
| category | ordinal |
| order | ordinal |
| measure | linear |

Also you can explicitly specify dimension type / scale within *dimensions* section:

```javascript
var plot = new tauCharts.Chart({
    data: [
        { name: "John", age: 30, gender: 'Male',   hasChild: true  },
        ...
        { name: "Mary", age: 22, gender: 'Female', hasChild: false }
    ],
    dimensions: {
        name    : { type: 'category', scale: 'ordinal' },
        age     : { type: 'measure' },
        gender  : { type: 'category' },
        hasChild: { type: 'category' }
    },
    type:  "scatterplot",
    ...
    x:     "gender",
    y:     "age",
    size:  "age",
    color: "hasChild"
});
```

#### Nested objects in DataSource

As you might notice from previous examples we used only primitive values in "data row" properties. Actually TauCharts API allows you to pass nested objects as well. But such an approach goes with additional settings which tune which property to use as identity and which to display on axis ticks.

This can be useful for visualizing complex entities which *potentially* can have non-unique names but have to be tracked by their unique identity.

Let's consider example where property *person* contains nested object with *pass* and *name* properties. It means we want to code persons by their passport number but display their first names on axis marks.

```javascript
{
    data: [
        { status: "married", person: { pass: 1, firstName: 'John'  }},
        { status: "single" , person: { pass: 2, firstName: 'John'  }},
        ...
        { status: "married", person: { pass: 5, firstName: 'Mary'  }}
    ],
    dimensions: {   // <------- dimensions
        person: {
            type : 'category',
            value: 'pass'        // NOTE: use [value] property
                                 // to map identity (pass) in dimensions
        }
        ...
    },
    ...
    x: "person",
    ...
    guide: {        // <------- visual guide
        x: { name: "firstName" } // NOTE: use [name] property
                                 // to map visual property (firstName)
                                 // to x axis ticks
    }
});
```

Also you can use nested objects to specify *ordered* dimensions. The principle is the same: codify order by one property and use another property as visual marker for better readability.

```javascript
{
    data: [
        { bugName: "Exception", severity: { id: 1, title: 'Worse to fix it'  }},
        { bugName: "Error 404", severity: { id: 2, title: 'Laught if notice'  }},
        ...
        { bugName: "Crash App", severity: { id: 5, title: 'Fix ASAP'  }}
    ],
    dimensions: {   // <------- dimensions
        severity: {
            type : 'order',
            value: 'id'          // NOTE: [value] property to map severity id
        }
        ...
    },
    ...
    x: "severity",
    ...
    guide: {        // <------- visual guide
        x: { name: "title" }     // NOTE: use [name] property
                                 // to map visual property (severity title)
                                 // to x axis ticks
    }
});
```

#### Specifying *Ordered* dimension

There is one more way to specify *ordered* dimension.
Using this method you should pass data property as a primitive type (string, boolean) but provide to dimension declaration an **order** array which specify ascending order for categories. Once you have in data some unknown categories they will be added to the tail of **order** in the order of appearance in the source data.

```javascript
{
    data: [
        { featureID: 1, priority: 'High'},
        { featureID: 2, priority: 'Low'},
        ...
        { featureID: 5, priority: 'So-so'},
        ...
        { featureID: 9, priority: 'to be done yesterday'},

        { featureID: 99, priority: 'Medium'},
    ],
    dimensions: {
        ...
        priority: {
            type: 'order',
            order: ['Low', 'Medium', 'High'] // ["So-so", "to be done yesterday"]
                                             // will be added to the end of order
        }
        ...
    },
    ...
});
```
