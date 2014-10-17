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

According to the conception the API requires source data to be provided in form of structured table which can be expressed in javascript as an array of same-typed objects (e.g. in example above: name, age, gender, hasChild).

NOTE: we plan to support X-Array format in the near future.
