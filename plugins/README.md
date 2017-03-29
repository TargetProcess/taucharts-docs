# Plugins

Taucharts have several plugins out of box:
* [Tooltip](tooltip.md)
* Legend
* Quick filter
* Trendline,
* Export
* Annotations
* Layers
* Floating axes

Here is a [sample](https://jsfiddle.net/6mdLrj6o/23/)

#### Writing a plugin

A plugin is a function, which returns an object, that can handle chart events, place content into chart panels or execute chart methods.
``` javascript
(function () {
  function ExtraPlugin(settings) {
    return {
        init: function (chart) {},
        destroy: function () {},
        onSpecReady: function () {},
        onRender: function () {}
        ...
    }
  };
  tauCharts.api.plugins.add('extra', ExtraPlugin);
})();

var chart = new tauCharts.Chart({
    ...
    plugins: [
        tauCharts.api.plugins.get('extra')({...})
    ]
});
```

[Simple plugin example](https://jsfiddle.net/6mdLrj6o/27/)
