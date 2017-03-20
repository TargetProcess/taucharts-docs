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

[example jsFiddle](https://jsfiddle.net/taucharts/q4ka1aw4/)

TauCharts requires the source data to be provided in a form of structured table which can be expressed in javascript as an array of same-typed objects (e.g. in example above: name, age, gender, hasChild).

By default TauCharts try to detect a dimension type which can be a category, order or measure.

* **Category**: Represents data that can't be compared. Let's say, list of countries or names.
* **Order**: As you might guess, represents data that can be ordered, but you can't say how bigger one value from the other. For example, you can say that Must Have is more important than Nice to Have, but you can't say that Must Have is twice as important.
* **Measure**: That is easy. You can compare these variables, add them, multiply them, etc.

Using dimension type TauCharts tries to find the most appropriate scale for a dimension. Here is a list of default scales for corresponding dimension types:

| type | scale |
| -- | -- |
| category | ordinal |
| order | ordinal |
| measure | linear |

You can explicitly specify dimension type / scale in *dimensions* section:

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


#### *Ordered* dimension

You should pass data property as a primitive type (string, boolean) and define an **order** array that provides the order of categories.

For example, we have *priority* property in the data. It can be ordered, but TauCharts don't have a clue how to do that. In *dimensions* section you describe *priority* as *order* and set ['Low', 'Medium', 'High'] order.

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

<!---

(((!!!NESTED OBJECTS ARE THE SOURCE OF OBJECTS AND COMPLEXITY!!!)))

#### Nested objects in DataSource (DEPRECATED)

In previous examples we used only primitive values in data.  TauCharts API allows you to pass nested objects as well. In this case you should specify which property is an identity and which property should be on axis ticks.

This can be useful for visualizing complex entities which *potentially* can have non-unique names but have to be tracked by their unique identity (for example, Cities are non-unique).

Let's check an example where property *person* contains nested object with *pass* and *firstName* properties. It means we want to encode persons by their passport number, but display their first names on axis marks.

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
            value: 'pass'               // NOTE: use [value] property
                                        // to map identity (pass) in dimensions
        }
        ...
    },
    ...
    x: "person",
    ...
    guide: {        // <------- visual guide
        x: { tickLabel: "firstName" }   // NOTE: use [name] property
                                        // to map visual property (firstName)
                                        // to x axis ticks
    }
});
```

You can use nested objects to specify *ordered* dimensions:

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
            value: 'id'             // NOTE: [value] property to map severity id
        }
        ...
    },
    ...
    x: "severity",
    ...
    guide: {        // <------- visual guide
        x: { tickLabel: "title" }   // NOTE: use [name] property
                                    // to map visual property (severity title)
                                    // to x axis ticks
    }
});
```
-->

#### Time-based dimensions

In TauCharts time-based data is expressed as *order* or *measure* dimension type on *period* or *time* scale.

```javascript
{
    data: [
        { createDate: "2014-10-02", ... },                  // short ISO
        { createDate: "2014-10-02T22:17:59+03:00", ... },   // full ISO
        { createDate: 1412208000000, ... },                 // tick (from 1970-01-01Z)
        { createDate: new Date(), ... },                    // javascript Date object
        ...
    ],
    dimensions: {
        // if you want to split timeline to some specific periods (day, week, quarter...)
        createDate: {
            type : 'order',
            scale: 'period'
        }
        // guide property sets 
        guide: {
            x:{ tickPeriod: 'quarter', tickFormat: 'day' }
            // tickPeriod indicates that every tick is a quarter, while tickFormat sets how tick value will be displayed
            // In this example we will have quarters with first day of the quarter: 01-Jan-2014, 01-Apr-2014, 01-Jul-2014, 01-Oct-2014...
        }

        ...
        // or
        ...
        // if you want to draw continuous timeline
        createDate: {
            type : 'measure',
            scale: 'time'
        }
        ...
    }
}
```

Accepted time data source values:
- javascript [Date object](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Date)
- javascript [tick](http://www.w3schools.com/jsref/jsref_gettime.asp) (amount of milliseconds from 1970-01-01Z)
- string date in [ISO 8601](https://en.wikipedia.org/wiki/ISO_8601) format (e.g. "2014-10-02T22:17:59+03:00")

The period size for *periodical* scale is specified using [tickPeriod](../basic/guide.md#tickperiod) propert. There is a set of pre-defined periods:
- day
- week (split timeline by sundays)
- month
- quarter
- year

Also you can define [custom periods](../plugins/customticks.md).

#####NOTE: the periodic scale operates with JavaScript Date objects in a LOCAL timezone. Make sure your data meets this requirement otherwise Taucharts automatically cast data values to browser timezone which can be a source of unobvious errors.

The *time* scale doesn't require special customization, you can use [d3-based time format specifiers](https://github.com/mbostock/d3/wiki/Time-Formatting#format) for *tickFormat* in scale *guide*.
