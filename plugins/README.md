Plugins are in progress, folks. Stay tuned.

List of future plugins:

* Regression lines
* Tooltips
* Axes projection
* Brushing
* Legend
* Datasource to CSV
* Click to element

#### How to add custom tick period

Period scale supports a set of pre-defined [period specifiers](../datasource/README.md#time-based-dimensions). While you can define your custom periods.

There is an extension point in tauCharts API:

```javascript
tauChart.api.tickPeriod.add("custom_period_name", {
    cast: function(d) { ... },
    next: function(d) { ... }
})
```

- **cast** method is used to transform an input date value to the date of the period beginning. The *cast* should be pure function (without side effects) which map any date from the period to the same period beginning date.
- **next** method takes a previous beginning of period and produce next period date.

For example, below we *cast* a date to the beginning of week which it belongs to and produce next week date by adding 7 days:

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
Another example which shows how to cast a date to the 2 hour period of the day (00, 02, 04 ... 22, 24) and produce next 2-hours period:

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

