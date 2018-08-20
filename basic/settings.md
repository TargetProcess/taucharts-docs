# Settings

Apart of chart guide there is a chart settings that control chart appearance and behavior. Settings can be set globally or apply to the particular chart instance.

```javascript
// Globally
Plot.globalSettings.xDensityPadding = 4;

// Locally
var chart = new Taucharts.Chart({
  ...
  settings: {
    xDensityPadding: 4
  }
});
```

#### fitModel

This setting defines which strategy to use to embed a chart into a container.

Possible values: **minimal** / **entire-view** / **fit-width** / **fit-height** / **normal** (default value).

See example:
https://jsfiddle.net/taucharts/9hzfoqop/

#### xDensityPadding / yDensityPadding

These settings control minimal padding between tick text and tick border on ordinal scale.
It is 0.25 by default.
See example where yDensityPadding is set to 30 and xDensityPadding is set to 1:
https://jsfiddle.net/taucharts/p3jtgt4j/

#### animationSpeed

Controls the duration of elements animation. By default it is `750` ms. Set `0` to disable animation.

#### asyncRendering

Setting `asyncRendering: true` will make a browser more responsive, when rendering charts with large amount of data and facets. See more info about asynchronous rendering [here](../advanced/performance.md).