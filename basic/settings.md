# Settings

Apart of chart guide there is a chart settings that control chart appearance and behavior. Settings can be set globally or apply to the particular chart instance.

```javascript
// Globally
Plot.globalSettings.xDensityPadding = 4;

// Locally
var chart = new tauCharts.Chart({
  ...
  settings: {
    xDensityPadding: 4
  }
});
```

#### xDensityPadding / yDensityPadding

These settings control minimal padding between tick text and tick border on ordinal scale.
It is 0.25 by default.
See example where yDensityPadding is set to 8 and xDensityPadding is set to 2:
