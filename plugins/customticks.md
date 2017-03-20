#### How to add custom tick period

Period scale supports a set of pre-defined [period specifiers](../datasource/README.md#time-based-dimensions). However, you can define your custom periods.

There is an extension point in tauCharts API:

```javascript
tauChart.api.tickPeriod.add("custom_period_name", {
    cast: function(d) { ... },
    next: function(d) { ... }
})
```

- **cast** method is used to transform an input date value to the date of the period start. The *cast* should be pure function (without side effects) which maps any date from the period to the same period start date.
- **next** method takes a previous period's start date and produces the next period date.

For example, below we *cast* a date to the start of a week which it belongs to and produces the next week date by adding 7 days:

```javascript
{
    cast: function (date) {
        date = new Date(date.setHours(0, 0, 0, 0));
        date = new Date(date.setDate(date.getDate() - date.getDay()));
        return date;
    },
    next: function (prevDate) {
        // add 7 days to previous date
        return new Date(prevDate.setDate(prevDate.getDate() + 7));
    }
}
```
Another example shows how to cast a date to the 2 hour period of the day (00, 02, 04 ... 22, 24) and produce next 2-hours period:

```javascript
{
    cast: function(date) {
        var hour = date.getHours();
        var nearest2HSegment = hour - hour % 2;
        return new Date(date.setHours(nearest2HSegment, 0, 0, 0));
    },
    next: function(prevDate) {
        var h2 = (2 * 60 * 60 * 1000);
        return new Date(prevDate.getTime() + h2);
    }
}
```

#### How to add a custom tick format

Axis guide supports a set of pre-defined and d3-based [tick formats](../basic/guide.md#tickformat). While you can easily define your custom named tick format.

There is an extension point in tauCharts API:

```javascript
tauChart.api.tickFormat.add("custom_tick_format", function(x) { ... })
```

A formatter is a function which takes a value and produces a formatted string.

For example, below we add "quarter" formatter which takes a date object and produces a quarter which this date belongs to (e.g. "Q1 2014"):

```javascript
tauChart.api.tickFormat.add("quarter", function(x) {
    var d = new Date(x);
    var m = d.getMonth();
    var q = (m - (m % 3)) / 3;
    return 'Q' + (q + 1) + ' ' + d.getFullYear();
})
```

Custom format specifiers are useful for ticks localization.

See example of such localization: https://jsfiddle.net/qvqn12zg/
